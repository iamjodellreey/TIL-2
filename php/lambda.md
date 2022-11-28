
# Lambda

This is a basic example on how to use anonymous functions.

```php
// same as array_filter
function filteredBySomething($items, $fn){
    $result = [];

    foreach($items as $item){
        if($fn($item)){
            $result[] = $item
        }
    }

    return $result;
}

array_filter($books, function(){
    return $books['author'] === 'Jodelle';
});

```
