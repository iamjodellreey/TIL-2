# File Storage

## Storing Files

### Automatic Streaming

Streaming files to storage offers significantly reduced memory usage. If you would like Laravel to automatically manage streaming a given file to your storage location, you may use the putFile or putFileAs method. This method accepts either an Illuminate\Http\File or Illuminate\Http\UploadedFile instance and will automatically stream the file to your desired location:

```php
$file = $request->file('file');
$path = 'users';
$fileName = $file->hashName();

Storage::disk('local')->putFileAs($path, $file, $fileName);
```

## Retrieving Files

The get method may be used to retrieve the contents of a file. The raw string contents of the file will be returned by the method. Remember, all file paths should be specified relative to the disk's "root" location:

The exists method may be used to determine if a file exists on the disk:

```php
if (Storage::disk('local')->exists('users/hashed.jpg')) {
    // ...
}
```

```php
$contents = Storage::get('users/hashed.jpg');
```

## Deleting Files

The delete method accepts a single filename or an array of files to delete:

```php
use Illuminate\Support\Facades\Storage;

Storage::delete('users/hashed.jpg');

Storage::delete(['users/hashed1.jpg', 'users/hashed2.jpg']);
```

### Delete directory

The deleteDirectory method may be used to remove a directory and all of its files:

```php
Storage::deleteDirectory($directory);
```

Reference: https://laravel.com/docs/8.x/filesystem#main-content
