# Rendering Components

## Inline Components

```php
<div>
    <livewire:show-posts />

    @livewire('show-posts')
</div>
```

Use dot (.) prefixed with the namespace if component is inside a sub-folder

```php
<livewire:nav.show-posts />
```

## Passing Parameters

We can pass data into a component by passing additional parameters into the <livewire: tag.

```php
<livewire:show-post :post="$post">

@livewire('show-post', ['post' => $post])
```

## Receiving Parameters

Livewire will automatically assign parameters to matching public properties.

```php
class ShowPost extends Component
{
    public $post;

    ...
}
```

If for whatever reason, this automatic behavior doesn't work well for, we can intercept parameters using the mount() method:

```php
class ShowPost extends Component
{
    public $title;
    public $content;

    public function mount($post)
    {
        $this->title = $post->title;
        $this->content = $post->content;
    }

    ...
}
```

Like a controller, you can inject dependencies by adding type-hinted parameters before passed-in ones.

```php
use \Illuminate\Session\SessionManager;

class ShowPost extends Component
{
    public $title;
    public $content;

    public function mount(SessionManager $session, $post)
    {
        $session->put("post.{$post->id}.last_viewed", now());

        $this->title = $post->title;
        $this->content = $post->content;
    }

    ...
}
```
Reference: https://laravel-livewire.com/docs/2.x/rendering-components

---

### Question:

When is it appropriate to use ?

```
<livewire:show-post :post="$post">
or
@livewire('show-post', ['post' => $post])
```

### Answer:

 There is no exact appropriate scenario on what to use, It just depends on the developer on what syntax to use. But mainly the first syntax will be mostly used since livewire blade directive is just an alternative.

---

### Shared by other developer:

When receiving parameters it is much better to use mount since livewire is still improving and sometimes the magic behind automatically assign values on parameters receive to properties does not work.
