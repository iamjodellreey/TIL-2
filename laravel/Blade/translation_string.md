# Defining Translation Strings

# Using Short Keys

Typically, translation strings are stored in files within the resources/lang directory. Within this directory there should be a subdirectory for each language supported by the application.

```
/resources
    /lang
        /en
            messages.php
        /es
            messages.php
```

All language files return an array of keyed strings.

```php
<?php

// resources/lang/en/messages.php

return [
    'welcome' => 'Welcome to our application',
];
```

# Using Translation Strings As Keys

For applications with heavy translation requirements, defining every string with a "short key" can become quickly confusing when referencing them in your views. For this reason, Laravel also provides support for defining translation strings using the "default" translation of the string as the key.

Translation files that use translation strings as keys are stored as JSON files in the resources/lang directory. For example, if your application has a Spanish translation, you should create a resources/lang/es.json file.

```json
{
    "I love programming.": "Me encanta programar."
}
```

# Retrieving Translation Strings

You may retrieve lines from language files using the __ helper function. The __ method accepts the file and key of the translation string as its first argument.

```php
{{ __('messages.welcome') }}

@lang('messages.welcome')
```

If the specified translation string does not exist, the __ function will return the translation string key. So, using the example above, the __ function would return messages.welcome if the translation string does not exist.
