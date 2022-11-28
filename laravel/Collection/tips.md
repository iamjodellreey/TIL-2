
## Don't filter by NULL in Collections

We can filter by NULL in Eloquent, but if we're filtering the collection further - filter by empty string, there's no "null" in that field anymore.

```php

// This works
$messages = Message::where('read_at is null')->get();

// Won’t work - will return 0 messages
$messages = Message::all();
$unread_messages = $messages->where('read_at is null')->count();

// Will work
$unread_messages = $messages->where('read_at', '')->count();

```

## Multiple Collection Methods in a Row

We can query all results with ->all() or ->get(), we may then perform various Collection operations on the same result, it won’t query database every time.

```php
$users = User::all();
echo 'Max ID: ' . $users->max('id');
echo 'Average age: ' . $users->avg('age');
echo 'Total budget: ' . $users->sum('budget');
```

## Higher order collection methods

Collections have higher order methods, this are methods that can be chained , like groupBy() , map() ... Giving us a fluid syntax. This example calculates the price per group of products on an offer.

```php
$offer = [
        'name'  => 'offer1',
        'lines' => [
            ['group' => 1, 'price' => 10],
            ['group' => 1, 'price' => 20],
            ['group' => 2, 'price' => 30],
            ['group' => 2, 'price' => 40],
            ['group' => 3, 'price' => 50],
            ['group' => 3, 'price' => 60]
        ]
];

$totalPerGroup = collect($offer['lines'])->groupBy('group')->map(fn($group) => $group->sum('price'));
```
