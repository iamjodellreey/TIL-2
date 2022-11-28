# Validation

Validation in Livewire is similar to form validation in Laravel. In short, Livewire provides a $rules property for setting validation rules on a per-component basis, and a $this->validate() method for validating a component's properties using those rules.

```php
class ContactForm extends Component
{
    public $name;
    public $email;

    protected $rules = [
        'name' => 'required|min:6',
        'email' => 'required|email',
    ];

    public function submit()
    {
        $this->validate();

        // Execution doesn't reach here if validation fails.

        Contact::create([
            'name' => $this->name,
            'email' => $this->email,
        ]);
    }
}

<form wire:submit.prevent="submit">
    <input type="text" wire:model="name">
    @error('name') <span class="error">{{ $message }}</span> @enderror

    <input type="text" wire:model="email">
    @error('email') <span class="error">{{ $message }}</span> @enderror

    <button type="submit">Save Contact</button>
</form>
```

Sometimes it's useful to validate a form field as a user types into it. Livewire makes "real-time" validation simple with the $this->validateOnly() method.

To validate an input field after every update, we can use Livewire's updated hook:

# Real-Time validation

```php
class ContactForm extends Component
{
    public $name;
    public $email;

    protected $rules = [
        'name' => 'required|min:6',
        'email' => 'required|email',
    ];

    public function updated($propertyName)
    {
        $this->validateOnly($propertyName);
    }

    public function saveContact()
    {
        $validatedData = $this->validate();

        Contact::create($validatedData);
    }
}

<form wire:submit.prevent="saveContact">
    <input type="text" wire:model="name">
    @error('name') <span class="error">{{ $message }}</span> @enderror

    <input type="text" wire:model="email">
    @error('email') <span class="error">{{ $message }}</span> @enderror

    <button type="submit">Save Contact</button>
</form>
```
