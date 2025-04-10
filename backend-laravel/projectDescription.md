# In this part we will be discussing in details about our backend project

We use laravel as our backend framework which is the free and open-source PHP-based web framework for building web applications.


## Key Features of Laravel:

1. Eloquent ORM – An intuitive and powerful database abstraction layer.
2. Blade Templating Engine – A simple yet powerful way to create dynamic HTML pages.
3. Routing System – Easily define application routes using a simple and expressive syntax.
4. Middleware – Handle HTTP requests efficiently with middleware layers.
5. Authentication & Authorization – Built-in authentication and role-based access control.
6. Task Scheduling – Automate repetitive tasks with Laravel’s built-in scheduler.
7. Queues & Event Broadcasting – Asynchronous job processing for better performance.
8. Testing Support – Built-in testing tools for writing unit and feature tests.
9. Security Features – Protection against SQL injection, XSS, CSRF, and other threats

## Why use Laravel?
Developer-Friendly: Laravel offers a clean and intuitive syntax.
Scalability: Easily scale your application with built-in features like caching and queues.
Rich Ecosystem: Laravel has an extensive ecosystem, including Laravel Mix, Nova, and Forge.
Community Support: A large and active community provides continuous improvements and support.

## Laravel working mechanism

Laravel follows a structured way of handling web applications using the MVC (Model-View-Controller) architecture. This separation ensures maintainability and scalability.

1. Routing (web.php & api.php)
Routes define how the application responds to requests.
Located in routes/web.php (for web routes) and routes/api.php (for API routes).

````php
use Illuminate\Support\Facades\Route;
use App\Http\Controllers\MyController;

Route::get('/example', [MyController::class, 'exampleFunction']);
````

2. Controllers
Controllers handle the logic for incoming requests.
Located in app/Http/Controllers/.

````php
namespace App\Http\Controllers;

use Illuminate\Http\Request;

class MyController extends Controller {
    public function exampleFunction() {
        return response()->json(['message' => 'Hello, Laravel!']);
    }
}
````

3. Middleware
Middleware filters requests before they reach the controller.
Located in app/Http/Middleware/.

````php
public function handle($request, Closure $next) {
    if (!auth()->check()) {
        return redirect('/login');
    }
    return $next($request);
}
````

4. Views (Blade Templating Engine)
Laravel uses Blade (.blade.php) for dynamic HTML rendering.
Located in resources/views/.

````html
<!DOCTYPE html>
<html>
<head>
    <title>My Laravel Page</title>
</head>
<body>
    <h1>{{ $title }}</h1>
</body>
</html>
````

5. Configuration & Environment Settings
config/ folder contains configuration files.
.env file holds environment-specific settings (database, API keys, etc.).



## Utilizing Laravel for our backend.

### Controllers


Since, we will only be fetching the data from the database and there will be no such request that will be updating our database, I tried to keep the backend minimal. i.e. I just created the  single controller named `PopulationController.php` inside the Http\Controllers directory. This directory contains all the functions that we have been using until now to fetch the data from the database.In the future if the project becomes huge, we might want to create the separate controllers based on our needs. Also, the idea is to keep the backend minimal, so I havenot use middleware to filter requests before they reach the controller. It would be necessary to implement this, if we are having the requirement to filter the request based on the user authentication or so.

Below are the list of all the functions written inside the controller to fetech the data that is shown in the graph and maps.Moreover, there are other functions that were commented and put on the bottom of the page which could be used in the future in various ways. Note, that currently all these functions are meant to be fetch from the single database table called `coded_census`. As the project grows larger, we can use other tables as well and write the function similar to these.

1. getPopulationByGenderGroups :
function to get the population by gender where the census year is dynamic

2. getPopulationByGenderAndMunicipality : 
function to get the population by gender where the census year is dynamic and also the city is dynamic

3. getPopulationByMaritalStatusBasedOnGender :
function to get the population by gender along with marital status, where original marital status were merged to show four variable in the population pyramid. The census year is dynamic aswell

4. getSinglePopulationByGenderGroups :
function to get the population by gender by referring to the marital status that denotes single population i.e. sivilstatus = 6 where the census year is dynamic.


5. getPopulationDependency : 
 function to get the depdendency ratio based on the dynamic census year

6. getPopulationByOccupation :
function to get the occupation(few based on the codes) based on the dynamic census year



### Database
Since we will only be retreiving the data from our existing database and we wont be performing any operations that modifies our database in any way, we simply aviod all the laravel specific workflow for factories, migrations and seeders. we simply put our SQlite database inside the database directory and fetch the data from their.

In our case, we simply put the database name `histlab_tables_copy_new.db`  inside the database directory and fetch our data from there.

### Routes
 Our api routes are defined inside the `web.ph` files. Below are the list of routes that we have been using so far , for our project.Moreover, there are also other routes which are commented at the bottom of the page. These could be used in the future.


 ````bash

 Route::get('/population-by-gender-group/{year}',  [PopulationController::class, 'getPopulationByGenderGroups']);
Route::get('/population-by-marital-group-based-on-gender/{year}',  [PopulationController::class, 'getPopulationByMaritalStatusBasedOnGender']);
Route::get('/single-population-by-gender-group/{year}',  [PopulationController::class, 'getSinglePopulationByGenderGroups']);



Route::get('/population-by-gender-group-municipality/{year}/{municipalityCode}', [PopulationController::class, 'getPopulationByGenderAndMunicipality']);
Route::get('/population-depdendency/{year}',  [PopulationController::class, 'getPopulationDependency']);
Route::get('/population-by-occupation/{year}',  [PopulationController::class, 'getPopulationByOccupation']);
Route::get('/population-by-citizenship/{year}',  [PopulationController::class, 'getPopulationByCitizenship']);
 ````


 ### .env 
 The environmen files contains the important configurations that we will need in order to run the backend locally ,and also when we deploy the backend to the production environment, we have to adjust the configurations accordinly.The current working configurations for the backend project to run locally  is given below:

 ````bash
 APP_NAME=Laravel
APP_ENV=local
APP_KEY=your-app-key
APP_DEBUG=true
APP_TIMEZONE=UTC
APP_URL=http://localhost

APP_LOCALE=en
APP_FALLBACK_LOCALE=en
APP_FAKER_LOCALE=en_US

APP_MAINTENANCE_DRIVER=file
# APP_MAINTENANCE_STORE=database

BCRYPT_ROUNDS=12

LOG_CHANNEL=stack
LOG_STACK=single
LOG_DEPRECATIONS_CHANNEL=null
LOG_LEVEL=debug

#SQlite part
DB_CONNECTION=sqlite
DB_DATABASE=C:\path-to-laravel-project\database\histlab_tables_copy_new.db
# DB_HOST=127.0.0.1
# DB_PORT=3306


DB_FOREIGN_KEYS=true
# DB_USERNAME=root
# DB_PASSWORD=

SESSION_DRIVER=file
SESSION_LIFETIME=120
SESSION_ENCRYPT=false
SESSION_PATH=/
SESSION_DOMAIN=null

BROADCAST_CONNECTION=log
FILESYSTEM_DISK=local
QUEUE_CONNECTION=database

CACHE_STORE=database
CACHE_PREFIX=

MEMCACHED_HOST=127.0.0.1

REDIS_CLIENT=phpredis
REDIS_HOST=127.0.0.1
REDIS_PASSWORD=null
REDIS_PORT=6379

MAIL_MAILER=log
MAIL_HOST=127.0.0.1
MAIL_PORT=2525
MAIL_USERNAME=null
MAIL_PASSWORD=null
MAIL_ENCRYPTION=null
MAIL_FROM_ADDRESS="hello@example.com"
MAIL_FROM_NAME="${APP_NAME}"

AWS_ACCESS_KEY_ID=
AWS_SECRET_ACCESS_KEY=
AWS_DEFAULT_REGION=us-east-1
AWS_BUCKET=
AWS_USE_PATH_STYLE_ENDPOINT=false

VITE_APP_NAME="${APP_NAME}"
 ````
