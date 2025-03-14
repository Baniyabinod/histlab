The project`s aim is to make historical population data accessible and engaging. We want researchers, students, and the general public to explore population trends over time. By visualizing historical population data through a user-friendly interface, our goal is to enhance understanding of long term demographic changes.

For this, we are using  laravel framework which is a free and open-source PHP-based web framework for building web applications.


Note that, we are using SQlite database now, which will be later migrated to the MySql database for the production in the Azure.


## Installation Instructions
Once you have all the prequisities in your machine, clone the project using this command:

`https://github.com/Baniyabinod/UiT-history-project-backend.git`

Navigate to the project directory 

`cd UiT-history-project-backend`

Install the dependensices using the composer

`composer install`

Then, finally you can run this command to run your project

`php artisan serve`


## Utilizing the .sql file received
A MySQL dump file (.sql) contains SQL commands that can recreate a database, including tables, indexes, and data. It is commonly used for database migrations or backups.

download the MySQL workbench from here>
MySQL Workbench is a GUI tool for managing MySQL databases. Before importing a database, you need to ensure that your MySQL server is running and accessible.

https://dev.mysql.com/downloads/workbench/



## step followed for deploymeny
Pre-deployment Checklist
1. Ensure All Dependencies Are Installed
Run the following command in your project root to make sure all required dependencies are installed:

composer install --no-dev --prefer-dist

output:
Installing dependencies from lock file
Verifying lock file contents can be installed on current platform.
Package operations: 0 installs, 0 updates, 33 removals
  - Removing theseer/tokenizer (1.2.3)
  - Removing symfony/yaml (v7.1.1)
  - Removing sebastian/version (5.0.1)
  - Removing sebastian/type (5.0.1)
  - Removing sebastian/recursion-context (6.0.2)
  - Removing sebastian/object-reflector (4.0.1)
  - Removing sebastian/object-enumerator (6.0.1)
  - Removing sebastian/lines-of-code (3.0.1)
  - Removing sebastian/global-state (7.0.2)
  - Removing sebastian/exporter (6.1.3)
  - Removing sebastian/environment (7.2.0)
  - Removing sebastian/diff (6.0.2)
  - Removing sebastian/complexity (4.0.1)
  - Removing sebastian/comparator (6.0.2)
  - Removing sebastian/code-unit-reverse-lookup (4.0.1)
  - Removing sebastian/code-unit (3.0.1)
  - Removing sebastian/cli-parser (3.0.2)
  - Removing phpunit/phpunit (11.3.1)
  - Removing phpunit/php-timer (7.0.1)
  - Removing phpunit/php-text-template (4.0.1)
  - Removing phpunit/php-invoker (5.0.1)
  - Removing phpunit/php-file-iterator (5.1.0)
  - Removing phpunit/php-code-coverage (11.0.6)
  - Removing phar-io/version (3.2.1)
  - Removing phar-io/manifest (2.0.4)
  - Removing nunomaduro/collision (v8.4.0)
  - Removing myclabs/deep-copy (1.12.0)
  - Removing mockery/mockery (1.6.12)
  - Removing laravel/sail (v1.31.1)
  - Removing laravel/pint (v1.17.2)
  - Removing hamcrest/hamcrest-php (v2.0.1)
  - Removing filp/whoops (2.15.4)
  - Removing fakerphp/faker (v1.23.1)
Generating optimized autoload files
> Illuminate\Foundation\ComposerScripts::postAutoloadDump
> @php artisan package:discover --ansi

   INFO  Discovering packages.

  laravel/sanctum ............................................................................................................................. DONE
  laravel/tinker .............................................................................................................................. DONE
  nesbot/carbon ............................................................................................................................... DONE
  nunomaduro/termwind ......................................................................................................................... DONE

52 packages you are using are looking for funding.
Use the `composer fund` command to find out more!

2. Generate the Application Key (if not already set)

Edit
php artisan key:generate

output:
   INFO  Application key set successfully.

3. Run Database Migrations (if needed)
If you have migrations that need to be applied to your SQLite database, run:

php artisan migrate
Since SQLite is a file-based database, ensure the database file exists before migrating.

output:
  INFO  Preparing database.

  Creating migration table ............................................................................................................ 15.90ms DONE

   INFO  Running migrations.

  0001_01_01_000000_create_users_table ................................................................................................ 46.38ms DONE
  0001_01_01_000001_create_cache_table ................................................................................................ 10.96ms DONE
  0001_01_01_000002_create_jobs_table ................................................................................................. 23.79ms DONE
  2024_09_19_094442_create_personal_access_tokens_table ................................................................................ 9.88ms DONE

  4. went to azure and created the web app.
  then added the following configurations in the App settings in environment varaibles>
Key: DB_CONNECTION
Value: sqlite

Key: DB_DATABASE
Value: /home/site/wwwroot/database.sqlite

5. then added the github as the source and build and deployed the application
6. then went to advance tools inside the development tools and opened kudo

problem with the SLite and azure described here
https://daniellethurow.com/blog/2020/4/21/azure-app-services-and-sqllite3

look here for the ftp method to host website.
https://www.youtube.com/watch?v=fpR1TtrheVE


back up default file

 you will get the default file here
 cd /etc/nginx/sites-available/

"
server {
    #proxy_cache cache;
        #proxy_cache_valid 200 1s;
    listen 8080;
    listen [::]:8080;
    # root /home/site/wwwroot;
    root /home/site/wwwroot/public; #changed for laravel
    index  index.php index.html index.htm;
    # server_name  example.com www.example.com;
    server_name histlabbackend-fkbxbmhkdbccf0hn.norwayeast-01.azurewebsites.net; #changed to put our server name
    port_in_redirect off;

    location / {            
        index  index.php index.html index.htm hostingstart.html;
        try_files $uri $uri/ /index.php?$query_string;
    }

    # redirect server error pages to the static page /50x.html
    #
    # error_page   500 502 503 504  /50x.html; #commented out for laravel so that laravel debug mode pages are shown
    location = /50x.html {
        root   /html/;
    }
    
    # Disable .git directory
    location ~ /\.git {
        deny all;
        access_log off;
        log_not_found off;
    }

    # Add locations of phpmyadmin here.
    location ~* [^/]\.php(/|$) {
        fastcgi_split_path_info ^(.+?\.[Pp][Hh][Pp])(|/.*)$;
        fastcgi_pass 127.0.0.1:9000;
        include fastcgi_params;
        fastcgi_param HTTP_PROXY "";
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        fastcgi_param PATH_INFO $fastcgi_path_info;
        fastcgi_param QUERY_STRING $query_string;
        fastcgi_intercept_errors on;
        fastcgi_connect_timeout         300; 
        fastcgi_send_timeout           3600; 
        fastcgi_read_timeout           3600;
        fastcgi_buffer_size 128k;
        fastcgi_buffers 4 256k;
        fastcgi_busy_buffers_size 256k;
        fastcgi_temp_file_write_size 256k;
    }
}"



# use this command to restart the nginx service
service nginx restart

to check if gender 0 is included from the database table. first I tried with database.sqlite in desktop
SELECT kjonn, COUNT(*) 
FROM coded_census 
WHERE kilde = 'census_1910' 
AND kommunenr = '1902'
GROUP BY kjonn;


both database.sqlite and histlab_tables_copy_new doesnot have gender 0. which means the database in azure should give data without gender 0


the problem was with the part where we had defined the gender as such  in the frontend and to fix it we need to handle both inter and string types
as shown below
before
"{#if data.gender === "1"}"
{#if femaleData.age_group === data.age_group && femaleData.gender === "2"}

after
"{#if data.gender === "1" || data.gender === 1}"
{#if femaleData.age_group === data.age_group && (femaleData.gender === "2" || femaleData.gender === 2)}


for the occupation code, this didnot work because, the occupation code was written as 06110 instead of 6110. so it might not work in the local versio now.

to load the site and test, the api is changed as shown below>
/api/population-by-marital-group-based-on-gender/${selectedYear}`

