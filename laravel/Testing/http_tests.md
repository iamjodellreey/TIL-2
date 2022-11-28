# Session / Authentication

Laravel provides several helpers for working with the session during HTTP testing. First, you may set the session data to a given array using the withSession method.

```php
<?php
class ExampleTest extends TestCase
{
    $fileData = [
        'first_name' => 'Rohan',
        'last_name' => 'William',
        'birthday' => '1997/01/07',
    ];

    public function testApplication()
    {
        $this
            ->actingAs($this->authUser)
            ->withSession(['uploaded_file' => $fileData])
            ->post(route('csv.upload'))
            ->assertStatus(302)
            ->assertSessionHas(['flash_success' => 'Csv was uploaded successfully.']);
    }
}
```
