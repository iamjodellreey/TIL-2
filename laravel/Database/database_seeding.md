# Database: Seeding

Laravel includes a simple method of seeding the database with test data using seed classes. All seed classes are stored in the database/seeds directory. Seed classes may have any name, but probably should follow some sensible convention, such as UserSeeder, etc. By default, a DatabaseSeeder class is defined. From this class, we may use the call method to run other seed classes, allowing us to control the seeding order.

### Generate a seeder

```php
php artisan make:seeder UserSeeder
```

### DatabaseSeeder class

```php
<?php

use Illuminate\Database\Seeder;
use Illuminate\Support\Facades\DB;
use Illuminate\Support\Facades\Hash;
use Illuminate\Support\Str;

class DatabaseSeeder extends Seeder
{
    /**
     * Run the database seeds.
     *
     * @return void
     */
    public function run()
    {
        DB::table('users')->insert([
            'name' => Str::random(10),
            'email' => Str::random(10).'@gmail.com',
            'password' => Hash::make('password'),
        ]);
    }
}
```

### Using model factories in seeders.

 Manually specifying the attributes for each model seed is cumbersome instead we can use model factories to conveniently generate large amounts of database records.

```php
/**
 * Run the database seeds.
 *
 * @return void
 */
public function run()
{
    factory(App\User::class, 50)->create()->each(function ($user) {
        $user->posts()->save(factory(App\Post::class)->make());
    });
}

```

### Calling additional seeder

Within the DatabaseSeeder class, we may use the call method to execute additional seed classes. Using the call method allows us to break up the database seeding into multiple files so that no single seeder class becomes overwhelmingly large.

```php
/**
 * Run the database seeds.
 *
 * @return void
 */
public function run()
{
    $this->call([
        UserSeeder::class,
        PostSeeder::class,
        CommentSeeder::class,
    ]);
}
```

### Running seeders

- Generate first Composer's autoloader using the dump-autoload command

```php
composer dump-autoload
```

Now we may use the db:seed Artisan command to seed the database. By default, the db:seed command runs the DatabaseSeeder class, which may be used to call other seed classes. However, we may use the --class option to specify a specific seeder class to run individually:

```php
php artisan db:seed

php artisan db:seed --class=UserSeeder
```

We may also seed the database using the migrate:fresh command, which will drop all tables and re-run all of migrations. This command is useful for completely re-building your database:

```php
php artisan migrate:fresh --seed
```

Reference

https://laravel.com/docs/7.x/seeding
