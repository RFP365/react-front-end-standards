# HTML Guidelines
> Through React, we typically deliver HTML in JSX form. Some manual HTML may exist outside of our default front-end stack.


https://developer.mozilla.org/en-US/docs/Learn/HTML/Introduction_to_HTML/Getting_started
## Attributes
```html
<div id="parent-component" >
    <span class="CSS-Selector"> Content </span>
    <button data-btn-id="3"> Click Me. </button>
</div>

```
### id
- Historically used for `.js` hooks & `.css` selectors.
- Now **ONLY** use them when appropriate for `component level hooks` or `third-party declaration`. Avoid Otherwise.
### class
- Used for Styling HTML. **NEVER** use as a javascript hook.
### data-attribute
- Used to de-couple markup/styling from javascript functionality. Use for .js selectors.
- Boolean data elements can be left blank. `<button class="clean" disabled />`
### style
Manual styling of markup directly. Favor using components instead adding one off mutations through style. 
This is an **(CODE-SMELL)**.

## General Guidelines
Full HTML overview is out of scope of company guidelines.
Outlined below will be some notables and pitfalls.
For further assistance, the web has plenty of [Documentation](https://developer.mozilla.org/en-US/docs/Learn/HTML/Introduction_to_HTML/Getting_started).

### Div vs. Span
When generic containers are needed, use `<div>` for block level elements and `<span>` for inline elements.

### Closing Tags
All elements should be closed via a tag pair or self closing declaration.

```html
<p>Lorem ipsum dolor sit amet, consectetur adipisicing elit.</p>
<p>Lorem ipsum dolor sit amet, consectetur adipisicing elit.</p>
<p>Lorem ipsum dolor sit amet, consectetur adipisicing elit.</p>
```

### Linting/Prettier
Thought is typically is given to `Brackets`, `Whitespace`, `semicolons`, `indentation`.
Due to Linting validation and pre-commit hook cleanup, these are largely obfuscated away.

## Accessibility Compliance
Needs Content
