```php
// Task 1: point the main "/" URL to the HomeController method "index"
// Put one code line here below
Route::get('/', [HomeController::class, 'index'])->name('dashboard');


// Task 2: point the GET URL "/user/[name]" to the UserController method "show"
// It doesn't use Route Model Binding, it expects $name as a parameter
// Put one code line here below
Route::get('/user/{name}', [UserController::class, 'show']);


// Task 3: point the GET URL "/about" to the view
// resources/views/pages/about.blade.php - without any controller
// Also, assign the route name "about"
// Put one code line here below
Route::view('/about', 'pages.about')->name('about');

// Task 4: redirect the GET URL "log-in" to a URL "login"
// Put one code line here below
Route::permanentRedirect('log-in', 'login');

// Task 5: group the following route sentences below in Route::group()
// Assign middleware "auth"
// Put one Route Group code line here below
Route::group(['middleware' => 'auth'], function(){

    // Tasks inside that Authenticated group:

    // Task 6: /app group within a group
    // Add another group for routes with prefix "app"
    // Put one Route Group code line here below
    Route::group(['prefix' => 'app'], function(){

        // Tasks inside that /app group:

        // Task 7: point URL /app/dashboard to a "Single Action" DashboardController
        // Assign the route name "dashboard"
        // Put one Route Group code line here below
        Route::get('/dashboard', DashboardController::class)->name('dashboard');

        // Task 8: Manage tasks with URL /app/tasks/***.
        // Add ONE line to assign 7 resource routes to TaskController
        // Put one code line here below
        Route::resource('/tasks', TaskController::class);

    // End of the /app Route Group
    });

    // Task 9: /admin group within a group
    // Add a group for routes with URL prefix "admin"
    // Assign middleware called "is_admin" to them
    // Put one Route Group code line here below
    Route::group(['prefix' => 'admin', 'middleware' => 'is_admin'], function(){

        // Tasks inside that /admin group:

        // Task 10: point URL /admin/dashboard to a "Single Action" Admin/DashboardController
        // Put one code line here below
        Route::get('/dashboard', AdminDashboardController::class);

        // Task 11: point URL /admin/stats to a "Single Action" Admin/StatsController
        // Put one code line here below
        Route::get('/stats', StatsController::class);

    // End of the /admin Route Group
    });
// End of the main Authenticated Route Group
});
// One more task is in routes/api.php
```

```php
Route::group(['middleware' => 'auth:sanctum'], function() {
    // Task 12: Manage tasks with endpoint /api/v1/tasks/*****.
    // Keep in mind that prefix should be /api/v1.
    // Add ONE line to assign 5 resource routes to TaskController
    // Put one code line here below
    Route::resource('/v1/tasks', TaskController::class);
});

```