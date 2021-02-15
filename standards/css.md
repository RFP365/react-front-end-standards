# CSS Guidelines

> We currently use Emotion(Styled Components) to style our React Components. Those are typically laid out within the javascript and not externalized. A file with too many lines, styles, or components is a good candidate for refactor.

Additional Info: [Emotion Documentation](https://emotion.sh/docs/styled)

---
## Example
```jsx
import styled from '@emotion/styled'

render(
    <Container column>
        <Button>This is a regular button.</Button>
        <Button primary>This is a primary button.</Button>
        <StyleDrawer className = {clsx({ active: isOpen })} />
    </Container>
)

const Button = styled.button`
color: ${props =>
    props.primary ? 'hotpink' : 'turquoise'};
`

const Container = styled.div(props => ({
    display: 'flex',
    flexDirection: props.column && 'column'
}))

const StyleDrawer = styled(Drawer)`
  width: ${variable.FULL}px;
  &.active {
    width: ${variable.FULL}px;
    background-color: ${({theme}) => theme.palette.gray.light};  
    }
  &.not-active {
    width: ${variable.MIN}px;
    background-color: ${({theme}) => theme.palette.gray.dark};  
    overflow-x: hidden;
  }
}`
```

## Structure/NamingConventions
### Components
- General Naming: Use Descriptive PascalCase Naming(EG: `BigButton`, `TopContent`). 
- When styling a root component use `Styled[RootComponent]` to avoid naming conflicts.
- Wrapping ThirdParty Components. Preface with Styled. IE. `Styled[ThirdPartyComponent]`

````jsx
const MainContent = styled.div`
    color: ${props => props.primary ? 'hotpink' : 'turquoise'};
`
````

### SubComponents
When laying out React components, try to compose in modular terms.
This will help in styling and often to break patterns for re-use.
When appropriate, add a post-fix to denote SubClassing of Component Styles.

```jsx
const MainContentBody = styled.div`
    /* Body Styles */
`

const MainContentTop = styled.div`
    /* Top Styles */
`
```

### Extensions
For small Extension, SubClasses, a scss nested class is acceptable.
For moderate modifiers create a new Component with a postfix modifier.
1) Using a SCSS Nested Class Modifier
````jsx
const BigButton = styled(Button)`
        //Original Styles
    &.outlined {
        //Outlined Specific Styles
    }`
````

2) Create new Extended Components
````jsx
const BugButtonOutlined = styled(BigButton)`
    /* Include Only Overwritting Styles */
}`

````

### Representing State
When toggling styles, create an `is` modified state variable. Such as `isActive`.
Target state by using a nested `&.active` or snake-case to overwrite styles.
````jsx
const BigButton = styled(Button)`
        /* Original Styles */
    &.open {
        /* Toggled State Styles */
    }
    &.is-closed {
        /* Toggled State Styles */
    }`
````

## General StyleSheet Guidelines
Full CSS overview is out of scope of company guidelines. 
Outlined below will be some notables and pitfalls. 
For further assistance, the web has plenty of [Documentation](https://developer.mozilla.org/en-US/docs/Learn/CSS/).

### Positioning
- Most elements should stick to a `Relative` positioning. 
- `Absolute` creates highly coupled design and is fragile to change. Use for limited scope positioning or global cases.

 Need greater control? There are a few options.
1) Use `FlexBox` or a modern CSS Layout Feature. (See: [Guide to Flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/))
2) Use a CSS Layout Framework such as `BootStrap`.

### Margin/Padding
Margin is used for spacing between components. Padding is used for spacing within a component.
Take advantage of the natural document flow when spacing content by trying to use only margin bottom on content elements so they can easily be interchanged while keeping a predictable document flow and avoiding margin collapsing issues.
Additionally use padding on containers to keep a consistent "edge".
```javascript
//Do this.
const StackableContent = styled.div`
    margin-bottom:15px;
`
// Intead of this.
const StackableContent = styled.div`
    margin-top:10px;
    margin-bottom:5px;
`
```

### References
Note: (Not as relevant with `Styled Components`)
- Use `class` whenever possible. It promotes a modular workflow.
- Never style using `id`. It is now a backup for data hookups. Use `data-[]` `id` first.
````html
//Use
<div class="CSS-Selector" ></div>
<div data-view-close ></div>
//Avoid
<div id="CSS-Selector"></div>
````

### Property Order
CSS properties should be grouped by commonality (display, then box-model, then positioning, then background/color, then typography, then misc/etc).
Not strongly enforced, but a good consideration.

### Common Variables
Always reference global variables for commonly used values.
Failure to re-use will result in error and an ever expanding list of one-offs.
Examples include `colors`, `fonts`, `spacing`.

### Using Material-UI Themes
If your component has been wrapped at a high-level with a ThemeProvider. Use the theme for common variables.
```
  background-color: ${({theme}) => theme.palette.gray.light};
  color: ${({ theme }) => theme.palette.primary.main};
  font-size: ${({ theme }) => theme.typography.pxToRem(12)};
  font-weight: ${({ theme }) => theme.typography.fontWeightBold};
```

### Linting/Prettier
Thought is typically is given to `Brackets`, `Whitespace`, `semicolons`, `indentation`.
Due to Linting validation and pre-commit hook cleanup, these are largely obfuscated away.


## Questions to Answer
Should we Have Separate Conventions for Extension vs. SubComponent.
