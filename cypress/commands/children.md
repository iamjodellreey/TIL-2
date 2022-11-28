# children

Get the children of each DOM element within a set of DOM elements.

### Usage

```js
cy.get('nav').children() // Yield children of nav
```

### Incorrect Usage

```js
cy.children() // Errors, cannot be chained off 'cy'
cy.location().children() // Errors, 'location' does not yield DOM element
```

### Example

```html
<div>
  <ul>
    <li class="active">Unit Testing</li>
    <li>Integration Testing</li>
  </ul>
</div>
```


```js
// yields [
//  <li class="active">Unit Testing</li>
// ]
cy.get('ul').children('.active')
```

### References

- [cypress children](https://docs.cypress.io/api/commands/children#No-Args)
