### Stubbing Window

- This is an example showing how to stub window object

The application index.html has a single button that executes window.open on click.

```js
describe('window open', function () {
  it('opens a new window with page1', function () {
    cy.visit('/index.html')
    cy.window().then((win) => {
      cy.stub(win, 'open').as('windowOpen')
    })
    cy.get('#open-window').click()
    cy.get('@windowOpen').should('be.calledWith', 'page1.html')
  })
})
```

This implementation stubs the window.open method using cy.stub(). Because the application executes window.open after the click we create the method stub after cy.visit.

### Stubbing Window Print

```html
<!doctype html>
<html>
  <head>
    <meta charset="utf-8">
    <title>Stubbing Window Print</title>
  </head>
  <body>
    <h1>Application</h1>
    <ul>
      <li>
        <button id="print-window">Print 🖨</button>
      </li>
    </ul>

    <script src="./app.js"></script>
  </body>
</html>
```

Html above calls window.print on button click.

```js
describe('window.print', () => {
  it('can be stubbed', () => {
    cy.visit('index.html')
    cy.window().then((win) => {
      cy.stub(win, 'print').as('print')
    })

    cy.get('#open-print').click()
    cy.get('@print').should('have.been.calledOnce')
  })
})
```

By stubbing the window.print the this implementation can confirm the call has happened.
