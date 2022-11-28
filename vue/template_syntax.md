# Template Syntax

Vue uses an HTML-based template syntax that allows you to declaratively bind the rendered DOM to the underlying component instance's data. All Vue templates are syntactically valid HTML that can be parsed by spec-compliant browsers and HTML parsers.

### Text Interpolation

The most basic form of data binding is text interpolation using the "Mustache" syntax (double curly braces):

```js
<span>Message: {{ msg }}</span>
```

The mustache tag will be replaced with the value of the msg property from the corresponding component instance. It will also be updated whenever the msg property changes.

### Raw HTML

The double mustaches interprets the data as plain text, not HTML. In order to output real HTML, you will need to use the v-html directive:

```js
<p>Using text interpolation: {{ rawHtml }}</p>
<p>Using v-html directive: <span v-html="rawHtml"></span></p>
```

```js
Using text interpolation: <span style="color: red">This should be red.</span>

Using v-html directive: This should be red.
```

### Attribute Bindings

Mustaches cannot be used inside HTML attributes. Instead, use a v-bind directive:

```js
<div v-bind:id="dynamicId"></div>
```

The v-bind directive instructs Vue to keep the element's id attribute in sync with the component's dynamicId property. If the bound value is null or undefined, then the attribute will be removed from the rendered element.

#### Shorthand

Because v-bind is so commonly used, it has a dedicated shorthand syntax:

```js
<div :id="dynamicId"></div>
```

### Boolean Attributes

Boolean attributes are attributes that can indicate true / false values by its presence on an element. For example, disabled is one of the most commonly used boolean attributes.

v-bind works a bit differently in this case:

```js
<button :disabled="isButtonDisabled">Button</button>
```

The disabled attribute will be included if isButtonDisabled has a truthy value. It will also be included if the value is an empty string, maintaining consistency with <button disabled="">. For other falsy values the attribute will be omitted.

#### Dynamically Binding Multiple Attributes

If you have a JavaScript object representing multiple attributes that looks like this:

```js
data() {
  return {
    objectOfAttrs: {
      id: 'container',
      class: 'wrapper'
    }
  }
}
```

You can bind them to a single element by using v-bind without an argument:

```js
<div v-bind="objectOfAttrs"></div>
```
