# Hashing

The Laravel Hash facade provides secure Bcrypt and Argon2 hashing for storing user passwords.
The default hashing driver for your application is configured in the config/hashing.php configuration file.

## Basic Usage

```php
<?php

namespace App\Http\Controllers;

use App\Http\Controllers\Controller;
use Illuminate\Http\Request;
use Illuminate\Support\Facades\Hash;

class UpdatePasswordController extends Controller
{
    /**
     * Update the password for the user.
     *
     * @param  Request  $request
     * @return Response
     */
    public function update(Request $request)
    {
        // Validate the new password length...

        $request->user()->fill([
            'password' => Hash::make($request->newPassword)
        ])->save();
    }
}
```

### Verifying a password against a hash

The check method allows you to verify that a given plain-text string corresponds to a given hash. However, if you are using the LoginController included with Laravel, you will probably not need to use this directly, as this controller automatically calls this method:

```php
if (Hash::check('plain-text', $hashedPassword)) {
    // The passwords match...
}
```

Possible Questions:

1. Is there a way to decrypt Hash passwords?

    A hash is one-way and provides no method for decryption. If the user forgot the password we should send the user a link to reset their password instead.

[Reference](https://stackoverflow.com/questions/32701107/how-to-decrypt-hash-password-in-laravel#:~:text=A%20hash%20is%20one%2Dway,link%20to%20reset%20their%20password.&text=You%20shall%20never%20store%20user's,Never%2C%20ever.)
