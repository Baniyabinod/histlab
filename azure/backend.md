# rhd-backend in Azure

Created the backend app service in Azure to host our laravel application. The new resource group was created automatically named as rhdtestprod with the location in Norway East.Linux operating system was used and by giving the name(rhd-backend), where the publising model was selected as the "Code"  and runtime stack was "php /8.2"

Once this was created, for the deployment, went into the deployment section where,the option to connect the github was available.I select my github account,sigin in  and then, selected the repo(https://github.com/Baniyabinod/UiT-history-project-backend).

The next step would be to save the configurations. After that the deployment is carried out automatically and then on the overview page, got the message that deployment was successful.


Then for the testing purpose, use this default domain name(rhd-backend-eufmcjg8c9hhekdd.norwayeast-01.azurewebsites.net) from the overview page into my svelte project inside `vite.config.js` which shows that the page was hosted without database for now.

````bash
import { sveltekit } from '@sveltejs/kit/vite';
import { defineConfig } from 'vite';

export default defineConfig({
    plugins: [sveltekit()],
    server: {
        proxy: {
          '/api': {
            target: 'rhd-backend-eufmcjg8c9hhekdd.norwayeast-01.azurewebsites.net',
            //rhd-backend-eufmcjg8c9hhekdd.norwayeast-01.azurewebsites.net
            //http://127.0.0.1:8000/
            changeOrigin: true,
            secure: false,
            rewrite: (path) => path.replace(/^\/api/, ''),
          },
        },
      },
});
````

Back up default file, which is most inportant for the laravel backend inside Azure. you will find it inside the directory shown below. you will need to go to the Development tools section on the left hand side of the Azure backend resource and then select SSH terminal. Once the terminal is opened, you will be able to see the default file inside that directory.
` cd /etc/nginx/sites-available/`

note that, we will be able to find the content of our backend inside this path when we are inside the terminal
`/home/site/wwwroot/`


````bash
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
}
````

Note, that any changes made in the backend server from the Azure portal or simple restart might change the configuration of the default file to its original state, so we need to be careful about this. And if by any chance the backend is not working, we need to fix it from this dafault file.

After you change the content inside the dafault file for the laravel, you need to restart the nginx server using this command given below.

`service nginx restart`
