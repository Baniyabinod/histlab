The project`s aim is to make historical population data accessible and engaging. We want researchers, students, and the general public to explore population trends over time. By visualizing historical population data through a user-friendly interface, our goal is to enhance understanding of long term demographic changes.

For this, we are using  laravel framework which is a free and open-source PHP-based web framework for building web applications.

Prerequities:
Below are the list of the softwares and tools that are required for the project
````bash
Composer version 2.7.8 2024-08-22 15:28:36
PHP version 8.3.11 (C:\php-8.3.11\php.exe)
Laravel Installer 5.8.3
````

in our project we are setting up the php version to be `8.2` inside the composer.json file as shown below.
````bash
 "require": {
        "php": "^8.2",
    },
````

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

