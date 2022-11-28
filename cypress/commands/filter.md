# filter

Get the DOM elements that match a specific selector.
Opposite of .not()

### Usage

```js
cy.get('td').filter('.users') // Yield all el's with class '.users'
```

### Incorrect Usage

```js
cy.filter('.animated') // Errors, cannot be chained off 'cy'
cy.location().filter() // Errors, 'location' does not yield DOM element
```

### Example

```html
<ul>
  <li>Home</li>
  <li class="active">About</li>
  <li>Services</li>
  <li>Pricing</li>
  <li>Contact</li>
</ul>
```


```js
// yields <li>About</li>
cy.get('ul').find('>li').filter('.active')
```

### References

- [cypress filter](https://docs.cypress.io/api/commands/filter#Selector)
