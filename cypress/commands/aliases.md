## Aliases

To access previous command values in before or beforeEach we use aliases.

```
beforeEach(() => {
  cy.button().then(($btn) => {
    const text = $btn.text()
  })
})

it('does not have access to text', () => {
  // how do we get access to text ?!?!
})
```

### Sharing Context

To alias something you'd like to share use the .as() command.

```
beforeEach(() => {
  // alias the $btn.text() as 'text'
  cy.get('button').invoke('text').as('text')
})

it('has access to text', function () {
  this.text // is now available
})
```

Under the hood, aliasing basic objects and primitives utilizes Mocha's shared context object: that is, aliases are available as this.\*.

Mocha automatically shares contexts for us across all applicable hooks for each test. Additionally these aliases and properties are automatically cleaned up after each test.

## Avoiding the use of this

Instead of using the this.\* syntax, there is another way to access aliases.

The cy.get() command is capable of accessing aliases with a special syntax using the @ character

```
beforeEach(() => {
  // alias the users fixtures
  cy.fixture('users.json').as('users')
})

it('utilize users in some way', function () {
  // use the special '@' syntax to access aliases
  // which avoids the use of 'this'
  cy.get('@users').then((users) => {
    // access the users argument
    const user = users[0]

    // make sure the header contains the first
    // user's name
    cy.get('header').should('contain', user.name)
  })
})
```

By using cy.get() we avoid the use of this.

There are use cases for both approaches because they have different ergonomics.

When using this.users we have access to it synchronously, whereas when using cy.get('@users') it becomes an asynchronous command.

cy.get('@users') is doing the same thing as cy.wrap(this.users).

Reference:
https://docs.cypress.io/guides/core-concepts/variables-and-aliases#Aliases
