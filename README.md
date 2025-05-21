
# ⚡ Laravel Cheat Sheet

Your ultimate one-stop guide to quickly reference the most essential Laravel commands, helpers, syntax, and workflows.

---

## 🧰 Artisan Commands

```bash
php artisan list                      # List all Artisan commands
php artisan serve                    # Start local development server
php artisan make:controller MyCtrl   # Create controller
php artisan make:model MyModel       # Create model
php artisan make:migration create_users_table
php artisan migrate                  # Run all migrations
php artisan migrate:rollback         # Rollback last migration batch
php artisan db:seed                  # Run seeders
php artisan tinker                   # REPL for testing Laravel code
php artisan route:list               # Display all routes
php artisan config:cache             # Cache the configuration
php artisan cache:clear              # Clear application cache
```

---

## 🗃️ File Structure Reference

| 📁 Task        | 📌 Path                              |
|---------------|--------------------------------------|
| Routes        | `routes/web.php`, `routes/api.php`   |
| Controllers   | `app/Http/Controllers/`              |
| Models        | `app/Models/`                        |
| Views         | `resources/views/`                   |
| Migrations    | `database/migrations/`               |
| Seeders       | `database/seeders/`                  |

---

## 🧭 Routing

```php
Route::get('/home', [HomeController::class, 'index']);
Route::post('/submit', fn() => 'Submitted!');
Route::put('/update/{id}', 'UserController@update');
Route::delete('/delete/{id}', 'UserController@destroy');

// Resource routes
Route::resource('users', UserController::class);

// Middleware example
Route::middleware(['auth'])->group(function () {
    Route::get('/dashboard', DashboardController::class);
});
```

---

## 🌱 Eloquent ORM

```php
// Read
User::all();
User::find($id);
User::where('email', $email)->first();

// Create
User::create(['name' => 'John', 'email' => 'john@example.com']);

// Update
$user = User::find($id);
$user->name = 'Updated';
$user->save();

// Delete
User::destroy($id);

// Relationships
$user->posts();         // hasMany
$post->user();          // belongsTo
$role->users();         // belongsToMany
```

---

## 📝 Blade Templating

```blade
{{-- Output --}}
{{ $user->name }}
{{ $user->email ?? 'N/A' }}

{{-- Conditionals --}}
@if($user)
  Welcome, {{ $user->name }}
@else
  Welcome, Guest
@endif

{{-- Loops --}}
@foreach($users as $user)
  <p>{{ $user->name }}</p>
@endforeach

{{-- Components --}}
@include('partials.nav')
@extends('layouts.app')

@section('content')
  <h1>Hello</h1>
@endsection
```

---

## ✅ Validation

```php
$request->validate([
    'name' => 'required|string|max:255',
    'email' => 'required|email|unique:users',
    'password' => 'required|min:6|confirmed',
]);
```

---

## 📂 Migrations

```php
Schema::create('users', function (Blueprint $table) {
    $table->id();
    $table->string('name');
    $table->string('email')->unique();
    $table->timestamps();
});
```

---

## 🔐 Authentication

```bash
composer require laravel/breeze --dev
php artisan breeze:install
npm install && npm run dev
php artisan migrate
```

Also supports:
- Jetstream
- Laravel UI
- Sanctum / Passport

---

## 🧮 Collections

```php
collect([1, 2, 3])->map(fn($n) => $n * 2);
collect([1, 2, 3])->filter(fn($n) => $n > 1);
collect([1, 2, 3])->sum();
collect([1, 2, 3])->avg();
```

---

## 🛠️ Laravel Helpers

```php
route('dashboard', ['id' => 1]);
asset('images/logo.png');
now();                              // Current timestamp
auth()->user();                     // Authenticated user
request()->input('email');         // Get request input
session(['key' => 'value']);       // Set session
session('key');                    // Get session
redirect()->route('home');         // Redirect
```

---

## ✉️ Sending Mail

```bash
php artisan make:mail WelcomeMail
```

```php
use App\Mail\WelcomeMail;
use Illuminate\Support\Facades\Mail;

Mail::to('user@example.com')->send(new WelcomeMail($data));
```

---

## 🪵 Logging

```php
use Illuminate\Support\Facades\Log;

Log::info('User logged in', ['id' => $user->id]);
Log::warning('Unusual activity detected');
Log::error('Something went wrong');
```

---

## 🧪 Testing

```bash
php artisan make:test UserTest
php artisan test
```

```php
public function test_user_can_register()
{
    $response = $this->post('/register', [
        'name' => 'Test User',
        'email' => 'test@example.com',
        'password' => 'password',
        'password_confirmation' => 'password',
    ]);

    $response->assertStatus(302);
}
```

---

## 🔧 Composer & NPM Essentials

```bash
composer install
composer update
composer dump-autoload

npm install
npm run dev      # Compile assets for dev
npm run build    # Compile assets for production
```

---

## ⚙️ .env Example

```env
APP_NAME=Laravel
APP_ENV=local
APP_KEY=base64:...
APP_DEBUG=true
APP_URL=http://localhost

DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=laravel
DB_USERNAME=root
DB_PASSWORD=

MAIL_MAILER=smtp
MAIL_HOST=smtp.mailtrap.io
MAIL_PORT=2525
MAIL_USERNAME=null
MAIL_PASSWORD=null
MAIL_ENCRYPTION=null
```

---

## 📚 Resources

- 📘 [Laravel Official Docs](https://laravel.com/docs)
- 🎓 [Laracasts](https://laracasts.com)
- 📰 [Laravel News](https://laravel-news.com)
- 🧩 [Packagist Laravel Packages](https://packagist.org)

---

> 💡 **Pro Tip:** Use `php artisan tinker` to experiment with Laravel code in real-time!

---

## 👏 Contribute

Feel free to fork this repo and submit pull requests with improvements. Let's build better Laravel tools together!

---

## 📄 License

MIT © [YourName](https://github.com/yourusername)
