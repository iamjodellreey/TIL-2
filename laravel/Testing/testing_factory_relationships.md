# Factory Relationships

## Has Many Relationships

 We can create a user that has three posts using the has method provided by the Laravel's factories. The has method accepts a factory instance:

```php
use App\Models\Post;
use App\Models\User;

$user = User::factory()
            ->has(Post::factory()->count(3))
            ->create();
```

We may explicitly specify the name of the relationship that you would like to manipulate:

```php
$user = User::factory()
            ->has(Post::factory()->count(3), 'posts')
            ->create();
```

Of course, we may perform state manipulations on the related models. In addition, we may pass a closure based state transformation if our state change requires access to the parent model:

```php
$user = User::factory()
            ->has(
                Post::factory()
                        ->count(3)
                        ->state(function (array $attributes, User $user) {
                            return ['user_type' => $user->type];
                        })
            )
            ->create();
```

### Using Magic Methods

For convenience, you may use Laravel's magic factory relationship methods to build relationships. For example, the following example will use convention to determine that the related models should be created via a posts relationship method on the User model:

```php
$user = User::factory()
            ->hasPosts(3)
            ->create();
```

When using magic methods to create factory relationships, you may pass an array of attributes to override on the related models:

```php
$user = User::factory()
            ->hasPosts(3, [
                'published' => false,
            ])
            ->create();
```

## Belongs To Relationships

The for method may be used to define the parent model that factory created models belong to. We can create three App\Models\Post model instances that belong to a single user:

```php
use App\Models\Post;
use App\Models\User;

$posts = Post::factory()
            ->count(3)
            ->for(User::factory()->state([
                'name' => 'Jessica Archer',
            ]))
            ->create();
```

If wealready have a parent model instance that should be associated with the models we are creating, we may pass the model instance to the for method:

```php
$user = User::factory()->create();

$posts = Post::factory()
            ->count(3)
            ->for($user)
            ->create();
```

### Using Magic Methods

```php
$posts = Post::factory()
            ->count(3)
            ->forUser([
                'name' => 'Jessica Archer',
            ])
            ->create();
```

## Many To Many Relationships

Like has many relationships, "many to many" relationships may be created using the has method:

```php
use App\Models\Role;
use App\Models\User;

$user = User::factory()
            ->has(Role::factory()->count(3))
            ->create();
```

### Pivot Table Attributes

This method accepts an array of pivot table attribute names and values as its second argument

```php
$user = User::factory()
            ->hasAttached(
                Role::factory()->count(3),
                ['active' => true]
            )
            ->create();
```

We may provide a closure based state transformation if our state change requires access to the related model:

```php
$user = User::factory()
            ->hasAttached(
                Role::factory()
                    ->count(3)
                    ->state(function (array $attributes, User $user) {
                        return ['name' => $user->name.' Role'];
                    }),
                ['active' => true]
            )
            ->create();
```

Reference: https://laravel.com/docs/8.x/database-testing#factory-relationships
