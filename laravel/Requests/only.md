
Update user credentials with condition if it also updated its password

```php
  $data = $request->only(['name', 'email']);

    if($password = $request->get('password')){
        $data['password'] = bcrypt($password);
    }

    auth()->user()->update($data);
```
