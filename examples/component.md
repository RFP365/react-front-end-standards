# Simple React Component Example

 Below is a simple react component. Notice that it is laid out with higher context up top and lower context below.
Borrowed from Vue.js, this layout keeps the 'component' at a glance. 
Complexity should be abstracted to helper methods/components and lifted out and put under the component.
Styles are abstracted to the very bottom and de-coupled from logic as much as possible.

---

````jsx
import React from 'react';
import PropTypes from 'prop-types';
import styled from '@emotion/styled';
import Button from '@material-ui/lab/Button';

import { CommonComponent } from '@rfp360-web/common-ui';
import { ChildComponent } from './child-component/ChildComponent';

/**
 * Simple description of the component and it's usage.
 * @param {Object} SimpleComponentProps
 * @param {boolean} SimpleComponentProps.individualProps Prop description
 */
const SimpleComponent = ({individualProps, children}) => {
    
    //OnSetup, OnChange Lifecycle Changes
    useEffect(() => {
        const loadData = async () => {
            //Some data loading logic.
        };
        loadData();
    }, []);
    
    //Local State Vars uses UseState hook.
    const [stateVar, setStateVar] = useState('defaultVal');

    //JSX Return
    return (
        <StyledSimpleComponent>
            <FunctionalChildComponent prop={'prop'}/>
            helperMethod();
        </StyledSimpleComponent>
    );
};

//PropTypes
SimpleComponent.propTypes = {
    individualProp: PropTypes.bool.isRequired,
};

//Abstracted javascript helper methods and components
const helperMethod = switchVar => {
    let toReturn = null;
    switch (switchVar) {
        case 1:
            toReturn = <>One</>;break;
        case 2:
            toReturn = <>Two</>;break;
    }
};

const FunctionalChildComponent = ({prop}) => (
    <div>{prop}</div>
)

//Styled Components
const StyledSimpleComponent = styled(Alert)`
width: 100%;
margin-bottom: ${({ theme }) => theme.spacing(3)}px;
`;

````

## Imports
Ordering. React > Frameworks > Library Imports > Local Imports

```javascript
import React from 'react';
import PropTypes from 'prop-types';
import styled from '@emotion/styled';
import Button from '@material-ui/lab/Button';

import { CommonComponent } from '@rfp360-web/common-ui';
import { ChildComponent } from './child-component/ChildComponent';
```

## JSDoc
JS Methods and React Components specifically should have some level of JSDOC documentation. There are many [Cheatsheets](https://devhints.io/jsdoc) available.
``` javascript
/**
* Description
* @param {Object} ComponentProps.
* @param {import('@rfp360-web/common-services').CompanyDto} ComponentProps.company
* @param {boolean} ComponentProps.isEnabled what does this do when toggled.
* @param {boolean} [ComponentProps.initialExpanded = false] if the tree item is initially expanded
* @param {(nodeId: string) => void} ComponentProps.itemSelected handle the click event
* @returns {React.FC}
*/
```
### Props
- Props are typically manually defined `({prop1, prop2})` to provide better propType visibility and enforcement.
- There are a few cases for destructuring `{[prop1, prop2} = props`, such as hooks.

### Returns
- Return JSX in only one location. If your element has a blank or invalid return. Use `null`.

### Guidelines 
## Common Usages
* useState: Hook used to store component state. (See: [useState Documentation](https://reactjs.org/docs/hooks-state.html))
* useEffect: Hook used to handle lifecycle changes. (OnSetup, OnChange, onUpdate ect.) (See: [useEffect Documentation](https://reactjs.org/docs/hooks-effect.html))
* Note: We are no longer using constructor, isMounted ect.. lifecycle methods.
## PropType
* Is required documentation and helps enforcement by React of incoming prop types.
* Complicated incoming props should receive `Shape`  Objects


### Related Style Guides
- React [See React Guidelines](../standards/react.md)
- Javascript/Functionality  [See JS Guidelines](../standards/js.md)
- Styling [See CSS Guidelines](../standards/css.md)




