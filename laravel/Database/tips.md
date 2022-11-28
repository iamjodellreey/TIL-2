## Raw DB Queries: havingRaw()

We can use RAW DB queries in various places, including havingRaw() function after groupBy().

```php
Product::groupBy('category_id')->havingRaw('COUNT(*) > 1')->get();
```
