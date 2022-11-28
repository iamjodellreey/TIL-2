## within

Scopes all subsequent cy commands to within this element. Useful when working within a particular group of elements such as a form in html.

#### Usage

```js
cy.get('.list').within(($list) => {}) // Yield the `.list` and scope all commands within it
```

#### Examples

```html
<form>
  <input name="email" type="email" />
  <input name="password" type="password" />
  <button type="submit">Login</button>
</form>
```

```js
cy.get('form').within(($form) => {
  // you have access to the found form via
  // the jQuery object $form if you need it

  // cy.get() will only search for elements within form,
  // not within the entire document
  cy.get('input[name="email"]').type('john.doe@email.com')
  cy.get('input[name="password"]').type('password')
  cy.root().submit()
})
```

```html
<table>
  <tr>
    <td>My first client</td>
    <td>My first project</td>
    <td>0</td>
    <td>Active</td>
    <td><button>Edit</button></td>
  </tr>
</table>
```

```js
cy.contains('My first client')
  .parent('tr')
  .within(() => {
    // all searches are automatically rooted to the found tr element
    cy.get('td').eq(1).contains('My first project')
    cy.get('td').eq(2).contains('0')
    cy.get('td').eq(3).contains('Active')
    cy.get('td').eq(4).contains('button', 'Edit').click()
  })
```


Reference:
https://docs.cypress.io/api/commands/within
