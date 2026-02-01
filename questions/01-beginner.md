# 🟢 Laravel Beginner Interview Questions (1-30)

### 1. What is the fundamental architecture pattern Laravel uses?
<details>
<summary><strong>View Answer</strong></summary>

Laravel follows the **MVC (Model-View-Controller)** architectural pattern.
- **Model:** Represents the data and business logic (Eloquent).
- **View:** The user interface (Blade templates).
- **Controller:** Handles user input and interactions between Model and View.
</details>

### 2. Explain the Directory Structure: What is the `public` folder for?
<details>
<summary><strong>View Answer</strong></summary>

The `public` directory is the **web root** of your application. It contains the `index.php` file, which is the entry point for all requests entering your application. It also houses your assets like images, JavaScript, and CSS.
</details>

### 3. What is the purpose of the `.env` file?
<details>
<summary><strong>View Answer</strong></summary>

The `.env` file handles **environment-specific configuration**. It stores sensitive credentials (database passwords, API keys) and settings that change between environments (Local, Staging, Production). It should **never** be committed to Git.
</details>

### 4. How do you define a Route that accepts a parameter?
<details>
<summary><strong>View Answer</strong></summary>

You define parameters using curly braces `{}`.

```php
Route::get('/user/{id}', function ($id) {
    return 'User ID: ' . $id;
});
```
</details/>

### 5. What is a Named Route and why use it?
<details> <summary><strong>View Answer</strong></summary>

A named route is a route with a specific alias/name.

Benefit: If you change the URL path later (e.g., /user/profile to /u/profile), you don't need to update your code everywhere, as route('profile') remains the same.
```php
Route::get('/user/profile', [UserController::class, 'show'])->name('profile');
```
</details>

### 6. What is Blade?
<details> <summary><strong>View Answer</strong></summary>

Blade is Laravel's powerful templating engine. Unlike other PHP templating engines, Blade does not restrict you from using plain PHP code in your views. Blade views are compiled into plain PHP code and cached until they are modified.

</details>

### 7. What is the difference between `{{ $data }}` and `{!! $data !!}` in Blade?
<details> <summary><strong>View Answer</strong></summary>

`{{ $data }}`: Echoes data after running htmlspecialchars() to prevent XSS attacks (Escaped).

`{!! $data !!}`: Echoes data as-is without escaping. Used for rendering HTML content (Unescaped).

</details>

### 8. What is a Migration?
<details> <summary><strong>View Answer</strong></summary>

Migrations are like version control for your database. They allow you to modify and share the application's database schema definition. You can run `php artisan migrate` to create tables and `php artisan migrate:rollback` to undo changes.

</details>

### 9. How do you roll back the last database migration?
<details> <summary><strong>View Answer</strong></summary>

You use the Artisan command:

```bash
php artisan migrate:rollback
```
To roll back all migrations, you use `php artisan migrate:reset`.
</details>

### 10. What is Eloquent ORM?
<details> <summary><strong>View Answer</strong></summary>

Eloquent is Laravel's default Object-Relational Mapper (ORM). It allows you to interact with your database using PHP syntax instead of writing raw SQL. Each database table has a corresponding "Model" (e.g., users table -> User model).

</details>

### 11. What is `$fillable` in an Eloquent Model?
<details> <summary><strong>View Answer</strong></summary>

`$fillable` is a property that defines a white-list of attributes that are allowed to be mass-assigned (e.g., using `create()` or `update()`). This protects against Mass Assignment vulnerabilities.

</details>

### 12. What is the alternative to `$fillable`?
<details> <summary><strong>View Answer</strong></summary>

The alternative is `$guarded`. It acts as a black-list, defining attributes that cannot be mass-assigned. If you set `protected $guarded = [];`, you make all attributes mass-assignable (use with caution).

</details>

### 13. How do you retrieve all rows from a table using Eloquent?
<details> <summary><strong>View Answer</strong></summary>

```php
$users = User::all();
```
</details>

### 14. What is a Seeder?
<details> <summary><strong>View Answer</strong></summary>

Seeders are classes used to populate your database with dummy or initial data. They are useful for setting up a development environment or populating tables like countries or roles.

</details>

### 15. What is a Model Factory?
<details> <summary><strong>View Answer</strong></summary>

Factories define a blueprint for generating fake data for your Models. They are typically used in testing or seeding to generate large amounts of dummy data quickly.

```php
User::factory()->count(50)->create();
```
</details>

### 16. What is Artisan?
<details> <summary><strong>View Answer</strong></summary>

Artisan is the command-line interface (CLI) included with Laravel. It provides helpful commands for common tasks like creating controllers, migrating databases, and running tests.

</details>

### 17. How do you create a new Controller via Artisan?
<details> <summary><strong>View Answer</strong></summary>
  
```bash 
php artisan make:controller UserController
```
</details>

### 18. What is Middleware?
<details> <summary><strong>View Answer</strong></summary>

Middleware provides a mechanism for inspecting and filtering HTTP requests entering your application. Common examples include checking if a user is logged in (`auth`), verifying CSRF tokens, or handling CORS.

</details>

### 19. What is CSRF protection and how does Laravel handle it?
<details> <summary><strong>View Answer</strong></summary>

Cross-Site Request Forgery (CSRF) is an attack that forces an authenticated user to execute unwanted actions. Laravel automatically generates a CSRF "token" for each active user session. You must include `@csrf` in your HTML forms to validate requests.

</details>

### 20. How do you validate a request in a Controller?
<details> <summary><strong>View Answer</strong></summary>

You can use the validate method provided by the Request object.

```php
$validated = $request->validate([
    'title' => 'required|unique:posts|max:255',
    'body' => 'required',
]);
```
</details>

### 21. What happens if validation fails in Laravel?
<details> <summary><strong>View Answer</strong></summary>

Laravel automatically redirects the user back to the previous location with all input and error messages flashed to the session. If it's an AJAX request, it returns a 422 JSON response.

</details>

### 22. What is the `App\Http\Kernel.php` file (or `bootstrap/app.php` in v11)?
<details> <summary><strong>View Answer</strong></summary>

It is the central location where Middleware is registered and configured. It handles the "Global" middleware stack (run on every request) and "Route" middleware groups (like `web` and `api`).

</details>

### 23. What is Route Model Binding?
<details> <summary><strong>View Answer</strong></summary>

It allows you to automatically inject model instances into your routes/controllers based on the ID in the URL.

```php 
// Instead of $id, type-hint the Model
Route::get('/users/{user}', function (User $user) {
    return $user->email;
});
```
</details>

### 24. What is a Resource Controller?
<details> <summary><strong>View Answer</strong></summary>

A Resource Controller creates all typical CRUD routes (index, create, store, show, edit, update, destroy) in a single line of code.

```php
Route::resource('photos', PhotoController::class);
```
</details>

### 25. How do you access the authenticated user?
<details> <summary><strong>View Answer</strong></summary>

You can use the `Auth` facade or the `auth()` helper.

```php 
$user = auth()->user();
// or
$user = Auth::user();
```
</details>

#### 26. What is the difference between `hasOne` and `belongsTo`?
<details> <summary><strong>View Answer</strong></summary>

hasOne: Used on the "Parent" model (e.g., User hasOne Phone). The foreign key is on the other table.

belongsTo: Used on the "Child" model (e.g., Phone belongsTo User). The foreign key is on this table.

</details>

### 27. What is `dd()`?
<details> <summary><strong>View Answer</strong></summary>

`dd()` stands for Dump and Die. It dumps the variable's contents to the browser and immediately stops the script execution. It is the most common debugging tool in Laravel.

</details>

### 28. Where are language files stored?
<details> <summary><strong>View Answer</strong></summary>

In Laravel 10, they are in resources/lang. In newer versions (and depending on publication), they might be in lang at the root. They store array keys for localization/translation.

</details>

### 29. What is a Service Provider?
<details> <summary><strong>View Answer</strong></summary>

Service Providers are the central place of all Laravel application bootstrapping. It is where you register bindings in the Service Container, event listeners, middleware, and routes.

</details>

### 30. How do you enable Maintenance Mode?
<details> <summary><strong>View Answer</strong></summary>

Using the Artisan command:

```bash
php artisan down
```
To bring it back online:

```bash
php artisan up
```
</details>





