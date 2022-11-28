## Validate dates with "now" or "yesterday" words

We can validate dates by rules before/after and passing various strings as a parameter, like: tomorrow, now, yesterday.

Example:

```php
$rules = [
    'start_date' => 'after:now',
    'end_date' => 'after:start_date'
];
```
