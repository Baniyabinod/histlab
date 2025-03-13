# In this part we will be discussing in details about our backend project

We use laravel as our backend framework which is the free and open-source PHP-based web framework for building web applications.


## Key Features of Laravel:

Eloquent ORM – An intuitive and powerful database abstraction layer.
Blade Templating Engine – A simple yet powerful way to create dynamic HTML pages.
Routing System – Easily define application routes using a simple and expressive syntax.
Middleware – Handle HTTP requests efficiently with middleware layers.
Authentication & Authorization – Built-in authentication and role-based access control.
Task Scheduling – Automate repetitive tasks with Laravel’s built-in scheduler.
Queues & Event Broadcasting – Asynchronous job processing for better performance.
Testing Support – Built-in testing tools for writing unit and feature tests.
Security Features – Protection against SQL injection, XSS, CSRF, and other threats

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

