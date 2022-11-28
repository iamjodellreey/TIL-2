# siblings

Get sibling DOM elements.

### Usage

```js
cy.get('td').siblings() // Yield all td's siblings
cy.get('li').siblings('.active') // Yield all li's siblings with class '.active'
```

### Incorrect Usage

```js
cy.siblings('.error') // Errors, cannot be chained off 'cy'
cy.location().siblings() // Errors, 'location' does not yield DOM element
```

### Example

```html
<ul>
  <li>Home</li>
  <li>Contact</li>
  <li class="active">Services</li>
  <li>Price</li>
</ul>
```


```js
// yields all other li's in list
cy.get('.active').siblings()
```

### References

- [cypress siblings](https://docs.cypress.io/api/commands/siblings#Usage)
