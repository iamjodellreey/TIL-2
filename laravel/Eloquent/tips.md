## Quickly output an Eloquent query in its SQL form

If you want to quickly output an Eloquent query in its SQL form, you can invoke the toSql() method onto it like so

```php
$invoices = Invoice::where('client', 'James pay')->toSql();

dd($invoices)
// select * from `invoices` where `client` = ?
```

## OrderBy on Eloquent relationships

We can specify orderBy() directly on your Eloquent relationships.

```php
public function products()
{
    return $this->hasMany(Product::class);
}

public function productsByName()
{
    return $this->hasMany(Product::class)->orderBy('name');
}
```

## Conditional relationships

If we use same relationship often with additional "where" condition, we can create a separate relationship method.

```php
public function comments()
{
    return $this->hasMany(Comment::class);
}

public function approved_comments()
{
    return $this->hasMany(Comment::class)->where('approved', 1);
}
```

## Use withCount() to Calculate Child Relationships Records

If wehave hasMany() relationship, and we want to calculate “children” entries, we don’t need to write a special query. For example, if we have posts and comments on our User model, we write this withCount():

```php
public function index()
{
    $users = User::withCount(['posts', 'comments'])->get();
    return view('users', compact('users'));
}
```

And then, in your Blade file, you will access those number with {relationship}_count properties:

```html
@foreach ($users as $user)
    <tr>
        <td>{{ $user->name }}</td>
        <td class="text-center">{{ $user->posts_count }}</td>
        <td class="text-center">{{ $user->comments_count }}</td>
    </tr>
@endforeach
```

## Eager Loading with Exact Columns

```php
$users = App\Book::with('author:id,name')->get();
```

## Check if Relationship Method Exists

```php
$user = User::first();
if (method_exists($user, 'roles')) {
	// Do something with $user->roles()->...
}
```

## We can add conditions to your relationships

```php
class User
{
    public function posts()
    {
        return $this->hasMany(Post::class);
    }

    // with a getter
    public function getPublishedPostsAttribute()
    {
        return $this->posts->filter(fn ($post) => $post->published);
    }

    // with a relationship
    public function publishedPosts()
    {
        return $this->hasMany(Post::class)->where('published', true);
    }
}
```
