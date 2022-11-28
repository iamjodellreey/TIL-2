# http_build_query

— Generates a URL-encoded query string from the associative (or indexed) array provided.

```php
http_build_query(
    array|object $data,
    string $numeric_prefix = "",
    ?string $arg_separator = null,
    int $encoding_type = PHP_QUERY_RFC1738
): string
```

#### data
    - May be an array or object containing properties.
    - If data is an array, it may be a simple one-dimensional structure, or an array of arrays (which in turn may contain other arrays).
    - If data is an object, then only public properties will be incorporated into the result.

#### numeric_prefix
    - If numeric indices are used in the base array and this parameter is provided, it will be prepended to the numeric index for elements in the base array only.

#### arg_separator
    - arg_separator.output is used to separate arguments but may be overridden by specifying this parameter.


#### encoding_type
    - By default, PHP_QUERY_RFC1738.
    - If encoding_type is PHP_QUERY_RFC1738, then encoding is performed per » RFC 1738 and the application/x-www-form-urlencoded media type, which implies that spaces are encoded as plus (+) signs.
    - If encoding_type is PHP_QUERY_RFC3986, then encoding is performed according to » RFC 3986, and spaces will be percent encoded (%20).

```php
$parametersList = [
    'foo' => 'bar',
    'baz' => 'boom',
    'cow' => 'milk',
    'null' => null,
    'php' => 'hypertext processor'
];

echo http_build_query($data) . "\n";
echo http_build_query($data, '', '&amp;');
```

The above example will output:

```
foo=bar&baz=boom&cow=milk&php=hypertext+processor
foo=bar&amp;baz=boom&amp;cow=milk&amp;php=hypertext+processor
```
