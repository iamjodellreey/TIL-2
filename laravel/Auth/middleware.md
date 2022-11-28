## Email Verification

```php
Route::view('/secretpage', 'secretpage')
    ->name('secretpage')->middleware('verified');
```

## Password Confirmation

```php
Route::view('/verysecretpage', 'verysecretpage')
    ->name('verysecretpage')->middleware('password.confirm');
```
