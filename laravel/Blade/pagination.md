# Database: Pagination

There are several ways to paginate items. The simplest is by using the paginate method on the query builder or an Eloquent query. The paginate method automatically takes care of setting the proper limit and offset based on the current page being viewed by the user.

```php
<?php

namespace App\Http\Controllers;

use App\Http\Controllers\Controller;
use Illuminate\Support\Facades\DB;

class UserController extends Controller
{
    /**
     * Show all of the users for the application.
     *
     * @return Response
     */
    public function index()
    {
        $users = DB::table('users')->paginate(15);

        return view('user.index', ['users' => $users]);
    }
}
```
