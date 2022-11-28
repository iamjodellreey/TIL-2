## root

Get the root DOM element.

#### Usage

```js
cy.root() // Yield root element <html>
cy.get('nav').within(($nav) => {
  cy.root() // Yield root element <nav>
})
```

```js
cy.get('form').within(($form) => {
  cy.get('input[name="email"]').type('john.doe@email.com')
  cy.get('input[name="password"]').type('password')
  cy.root().submit() // submits the form yielded from 'within'
})
```

Reference:
https://docs.cypress.io/api/commands/root
