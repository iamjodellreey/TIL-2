### Magic Actions

In Livewire, there are some "magic" actions that are usually prefixed with a "$" symbol:

```
$refresh	                Will re-render the component without firing any action
$set('property', value)	    Shortcut to update the value of a property
$toggle('property')	        Shortcut to toggle boolean properties on or off
$emit('event', ...params)	Will emit an event on the global event bus, with the provided params
$event	                    A special variable that holds the value of the event fired that triggered the
                            action.  Example usage: wire:change="setSomeProperty($event.target.value)"
```

Before

```php
// In component
public function resetName($name)
{
    $this->name = $name;
}

// In views
<form action="#" wire:submit="resetName('Jodelle')">
    <button>Reset Name</button>
</form>
```

After
```php
<form action="#" wire:submit.prevent="$set('name', 'Jodelle')">
    <button>Reset Name</button>
</form>
```

### Route Model Binding

PHP 7.4 up, you can also typehint class properties, and Livewire will automatically route-model bind to them. The following component's $post property will be automatically injected with no need for the mount() method.

```php
class ShowPost extends Component
{
    public Post $post;
}
```
