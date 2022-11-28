# Create Artisan Commands in Laravel

## Generating Commands

To create a new command, you may use the make:command Artisan command. This command will create a new command class in the app/Console/Commands directory.
You can check all possible artisan commands available by `php artisan list`

```php
php artisan make:command CreateStaffCommand
```

```php
<?php

//After creating it will create the class inside this folder
namespace App\Console\Commands;

use Illuminate\Console\Command;

class CreateStaffCommand extends Command
{
    /**
     * The name and signature of the console command.
     * How would you call the command.
     *
     * @var string
     */
    protected $signature = 'command:name';

    /**
     * The console command description.
     *
     * @var string
     */
    protected $description = 'Command description';

    /**
     * Create a new command instance.
     * We may use this to pass parameters
     * We can delete this if we don't want to use this.
     *
     * @return void
     */
    public function __construct()
    {
        parent::__construct();
    }

    /**
     * Execute the console command.
     * This handles what you want to do with the artisan command.
     * @return int
     */
    public function handle()
    {
        //Return 0 means success or we can tweak this by just showing something in the command
        return 0;

        //Showing something after executing command
        $this->info('Something');
    }
}
```

We can create staff by executing this command `php artisan staff:create`

```php
<?php

//After creating it will create the class inside this folder
namespace App\Console\Commands;

use Illuminate\Console\Command;

class CreateStaffCommand extends Command
{
    /**
     * The name and signature of the console command.
     *
     * @var string
     */
    protected $signature = 'staff:create';

    /**
     * The console command description.
     * @var string
     */
    protected $description = 'Staff Creation';

    /**
     * Create a new command instance.
     *
     * @return void
     */
    public function __construct()
    {
        parent::__construct();
    }

    /**
     * Execute the console command.
     *
     * @return int
     */
    public function handle()
    {

        Staff::create([
            'name' => 'Jodelle',
            'email' => 'jodelle_staff@gmail.com',
            'password' => bcrypt('secret'),
        ]);

        return 0;
    }
}
```

### Passing arguments in artisan commands

```php
  protected $signature = 'staff:create {name} {email} {password}';

   public function handle()
    {

        Staff::create([
            'name' => $this->argument('name'),
            'email' => $this->argument('email'),
            'password' => $this->argument('password'),
        ]);

    }


  //If arguments is optional

   protected $signature = 'staff:create {name?} {email?} {password?}';

   $password = Str::random(8);

   Staff::create([
            'name' => $this->argument('name') ?? $this->faker->name,
            'email' => $this->argument('email') ?? $this->faker->email,
            'password' => $this->argument('password') ?? bcrpyt($password),
        ]);
```

### Programmatically Executing Commands

Sometimes you may wish to execute an Artisan command outside of the CLI. For example, you may wish to execute an Artisan command from a route or controller or anywhere.
You may use the call method on the Artisan facade to accomplish this. The call method accepts either the command's signature name or class name as its first argument, and an array of command parameters as the second argument. The exit code will be returned:

```php
use Illuminate\Support\Facades\Artisan;

class StaffController extends Controller{

    public function createStaffUsingArtisanCommand()
    {
        $name = $this->faker->name;
        $email = $this->faker->email;
        $password = bcrypt(Str::random(8));

        Artisan::call('create:staff',[
            'name' => $name,
            'email' => $email,
            'password' => $password,
        ]);

        //and so on..
    }

}
```


Reference : https://laravel.com/docs/8.x/artisan
