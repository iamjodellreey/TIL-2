# Parent

Get the parent DOM element of a set of DOM elements.
Please note that .parent() only travels a single level up the DOM tree as opposed to the .parents() command.

### Usage

```js
cy.get('header').parent() // Yield parent el of `header`
```

### Incorrect Usage

```js
cy.parent() // Errors, cannot be chained off 'cy'
cy.reload().parent() // Errors, 'reload' does not yield DOM element
```

### Example

```js
<ul class="main-nav">
  <li>Overview</li>
  <li>
    Getting started
    <ul class="sub-nav">
      <li>Install</li>
      <li class="active">Build</li>
      <li>Test</li>
    </ul>
  </li>
</ul>
```


```js
// yields .sub-nav
cy.get('li.active').parent()
```

### References

- [cypress parent](https://docs.cypress.io/api/commands/parent#Syntax)
