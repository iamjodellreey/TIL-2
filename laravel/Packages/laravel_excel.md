# Laravel Excel

 Laravel Excel is intended at being Laravel-flavoured PhpSpreadsheet: a simple, but elegant wrapper around PhpSpreadsheet with the goal of simplifying exports and imports.

## Laravel Excel Features
- Easily export collections to Excel.
- Export queries with automatic chunking for better performance.
- Queue exports for better performance.
- Easily export Blade views to Excel.
- Easily import to collections.
- Read the Excel file in chunks.
- Handle the import inserts in batches.

### Laravel Import

To add UserImport class we execute this command:

```php
php artisan make:import UsersImport --model=User
```

The file can be found in app/Imports:

```
.
├── app
│   ├── Imports
│   │   ├── UsersImport.php
│
└── composer.json
```

The collection method will receive a collection of rows. A row is an array filled with the cell values.
We use WithHeadingRow to use the csv heading row as array keys of each row.

```php
<?php

namespace App\Imports;

use App\Models\User;
use Maatwebsite\Excel\Concerns\ToCollection;
use Maatwebsite\Excel\Concerns\WithHeadingRow;

class UsersImport implements ToCollection, WithHeadingRow
{
    public function collection(Collection $rows)
    {
        foreach ($rows as $row)
        {
            User::create([
                'family_name' => $row['family_name'],
                'first_name' => $row['first_name'],
                'email' => $row['email'],
            ]);
        }
    }
}
```

```php
use App\Imports\UsersImport;
use Maatwebsite\Excel\Facades\Excel;
use App\Http\Controllers\Controller;
use App\Http\Requests\User\CSVRequest;

class UsersController extends Controller
{
    public function import(CSVRequest $request)
    {
        Excel::import(new UsersImport, $request->file('file'));

        return redirect('/')->with('success', 'All good!');
    }
}
```

### Laravel Export

```
php artisan make:export UsersExport --model=User
```

#### Multiple Sheets

```
To allow the export to have multiple sheets, the WithMultipleSheets concern(interface) should be used. The sheets() method expects an array of sheet export objects to be returned.
```

```php
namespace App\Exports;

use Maatwebsite\Excel\Concerns\Exportable;
use Maatwebsite\Excel\Concerns\WithMultipleSheets;

class UserSheet implements WithMultipleSheets
{
    //This trait will make the export class exportable
    use Exportable;

    //Always remember that the order of the index matters to the order of the sheets in the file
    /**
     * @return array
     */
    public function sheets(): array
    {
        return [
            new InformationSheet(),
            new PaymentsSheet(),
        ];
    }
}

//Information Sheet
namespace App\Exports\Sheets;

use App\Models\Information;
use Maatwebsite\Excel\Concerns\FromCollection;
//This will autosize the cell according to header length
use Maatwebsite\Excel\Concerns\ShouldAutoSize;

class InformationExport implements FromCollection
{
    public function collection()
    {
        return Information::all();
    }
}

//Payments Sheet
namespace App\Exports\Sheets;

use App\Models\Payments;
use Maatwebsite\Excel\Concerns\FromCollection;

class PaymentsExport implements FromCollection
{
    public function collection()
    {
        return Payments::all();
    }
}
```

#### Mapping data

```php
use Maatwebsite\Excel\Concerns\FromArray;
use Maatwebsite\Excel\Concerns\WithMapping;
use Maatwebsite\Excel\Concerns\WithHeadings;

class Information implements FromArray, WithMapping, WithHeadings
{

    public function array(): array
    {
        $users = [
            [
                'first_name' => 'Stephen',
                'last_name' => 'Curry',
            ],
            [
                'first_name' => 'Klay',
                'last_name' => 'Thompson',
            ],
        ];

        return [$users];
    }

    //By adding WithMapping you map the data that needs to be added as row.
    public function map($rows): array
    {
        $firstNameOnly = [];
        foreach ($rows as $row) {
            $firstNameOnly[] = $row['first_name'];
        }

       return $firstNameOnly;
    }

    //heading row can easily be added by adding the WithHeadings concern.
    public function headings(): array
    {
        return [
            'First Name',
        ];
    }
}
```
