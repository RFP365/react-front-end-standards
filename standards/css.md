# React Front End Guidelines

## Overview
We currently use Emotion(Styled Components) to style our React Components.
Those are typically defined within a component. 
A file with too many lines, styles, or components is a good candidate for refactor.

Additional Info: [Emotion Documentation](https://emotion.sh/docs/styled)

## Structure/NamingConventions
### Components
- General Naming: Use Descriptive PascalCase Naming(EG: `BigButton`, `TopContent`). 
- When styling a root component use `Styled{RootComponent}` to avoid naming conflicts.
- Wrapping ThirdParty Components. Preface with Styled. IE. `Styled{ThirdPartyComponent}`


````javascript
const MainContent = styled.div`
    color: ${props => props.primary ? 'hotpink' : 'turquoise'};
`
````

## SubComponents
When laying out React components, try to compose in modular terms.
This will help in styling and often to break patterns for re-use.
When appropriate, add a post-fix to denote SubClassing of Component Styles.

```javascript
const MainContentBody = styled.div`
    //Body Styles
`

const MainContentTop = styled.div`
    //Top Styles
`
```

## Extensions
For small Extension, SubClasses, a scss nested class is acceptable.
For moderate modifiers create a new Component with a postfix modifier.
1) Using a SCSS Nested Class Modifier
````javascript
const BigButton = styled(Button)`
        //Original Styles
    &.outlined {
        //Outlined Specific Styles
    }`
````

2) Create new Extended Components
````javascript
const BugButtonOutlined = styled(BigButton)`
    //Include Only Overwritting Styles
}`

````

## Representing State
When toggling styles, create an `is` modified state variable.
Target state by using a nested `&.isVariable` to overwrite styles.
````javascript
const BigButton = styled(Button)`
        //Original Styles
    &.isOpen {
        //Toggled State Styles
    }`
````


### Example
```javascript
import styled from '@emotion/styled'

render(
    <Container column>
        <Button>This is a regular button.</Button>
        <Button primary>This is a primary button.</Button>
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
  &.drawer-open {
    width: ${variable.FULL}px;
    background-color: ${({theme}) => theme.palette.gray.light};  
    }
  &.drawer-closed {
    width: ${variable.MIN}px;
    background-color: ${({theme}) => theme.palette.gray.dark};  
    overflow-x: hidden;
  }
}`
```

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

### Common Variables
Always reference global variables for commonly used values.
Failure to re-use will result in error and an ever expanding list of one-offs.
- Examples include `colors`, `fonts`, `spacing`.

### Property Order
CSS properties should be grouped by commonality (display, then box-model, then positioning, then background/color, then typography, then misc/etc).
Not strongly enforced, but a good consideration.

### Linting/Prettier
Thought is typically is given to `Brackets`, `Whitespace`, `semicolons`, `indentation`.
Due to Linting validation and pre-commit hook cleanup, these are largely obfuscated away.

### Using our Themes
```
  background-color: ${({theme}) => theme.palette.gray.light};
  color: ${({ theme }) => theme.palette.primary.main};
  font-size: ${({ theme }) => theme.typography.pxToRem(12)};
  font-weight: ${({ theme }) => theme.typography.fontWeightBold};
```

## Questions to Answer
Should we Have Separate Conventions for Extension vs. SubComponent.
