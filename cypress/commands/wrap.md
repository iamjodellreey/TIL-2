# Wrap

Yield the object passed into .wrap(). If the object is a promise, yield its resolved value. Wrap requires being chained off of cy.

### Usage

```
cy.wrap({ name: 'Jane Lane' })
```

- Objects

```
const getName = () => {
  return 'Jane Lane'
}

cy.wrap({ name: getName }).invoke('name').should('eq', 'Jane Lane') // true
```

- Elements

```
cy.get('form').within(($form) => {
  // ... more commands

  cy.wrap($form).should('have.class', 'form-container')
})
```

- Conditionally wrap elements

```
cy.get('button').then(($button) => {
  // $button is a wrapped jQuery element
  if ($button.someMethod() === 'something') {
    // wrap this element so we can
    // use cypress commands on it
    cy.wrap($button).click()
  } else {
    // do something else
  }
})

```

### References

- [cypress wrap](https://docs.cypress.io/api/commands/wrap#Requirements)
