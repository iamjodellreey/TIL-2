# Each

Iterate through an array like structure (arrays or objects with a length property).

### Usage

```js
cy.get('ul>li').each(() => {...}) // Iterate through each 'li'
cy.getCookies().each(() => {...}) // Iterate through each cookie
```

### Incorrect Usage

```js
cy.each(() => {...})            // Errors, cannot be chained off 'cy'
cy.location().each(() => {...}) // Errors, 'location' doesn't yield an arra
```

### Example

```js
cy.get("ul>li").each(($el, index, $list) => {
  // $el is a wrapped jQuery element
  if ($el.someMethod() === "something") {
    // wrap this element so we can
    // use cypress commands on it
    cy.wrap($el).click();
  } else {
    // do something else
  }
});
```

```html
<ul>
  <li>10</li>
  <li>5</li>
  <li>6</li>
</ul>
```

```js
const list = [];
cy.get("li")
  .each(($li) => {
    list.push(parseInt($li.text()));
  })
  .wrap(list)
  .should("deep.equal", [10, 5, 6]);
```

### References

- [cypress each](https://docs.cypress.io/api/commands/each#DOM-Elements)
