## The Loop Variable in foreach

While iterating through a foreach loop, a $loop variable will be available inside of your loop.

```php
@foreach ($users as $user)
    @if ($loop->first)
        This is the first iteration.
    @endif

    @if ($loop->last)
        This is the last iteration.
    @endif

    <p>This is user {{ $user->id }}</p>
@endforeach
```

If you are in a nested loop, you may access the parent loop's $loop variable via the parent property

```php
@foreach ($users as $user)
    @foreach ($user->posts as $post)
        @if ($loop->parent->first)
            This is the first iteration of the parent loop.
        @endif
    @endforeach
@endforeach
```

Available loop properties

| Property             | Description                                           |
| -------------------- | ------------------------------------------------------|
| $loop->index         | The index of the current loop iteration (starts at 0).|
| $loop->iteration     | The current loop iteration (starts at 1).             |
| $loop->remaining     | The iterations remaining in the loop.                 |
| $loop->count         | The total number of items in the array being iterated.|
| $loop->first         | Whether this is the first iteration through the loop. |
| $loop->last          | Whether this is the last iteration through the loop.  |
| $loop->even          | Whether this is an even iteration through the loop.   |
| $loop->odd           | Whether this is an odd iteration through the loop.    |
| $loop->depth         | The nesting level of the current loop.                |
| $loop->parent        | When in a nested loop, the parent's loop variable.    |

## Blade @auth

```php
@if(auth()->user())
    // The user is authenticated.
@endif
```

```php
@auth
    // The user is authenticated.
@endauth
```

## Blade format date

```php

App\Models\User;

// add protected dates array with field that you want to be automatically carbon object
protected $dates = ['enrolled'];


// in blade you can directly call carbon methods.

{{ $user->enrolled->format('Y-m-d') }}
```

## forelse

```php
@forelse()
// do some thing if array is not empty
@empty
// If array is empty
@endforelse

```

## clear view php

```php
php artisan view:clear
```
