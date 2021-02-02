# React Component Example

Below is a simple react component. Notice that it is laid out with higher context up top and lower context below.
Borrowed from Vue.js, this layout keeps the 'component' at a glance. Complexity should be abstracted to helper methods/components.
Styles are abstracted to the very bottom and de-coupled from Logic when possible.

````javascript
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
    
    //Local State Vars
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

//Javascript helper methods and components
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

export default AuthFailureAlert;
````

## Imports
* Ordering. React > Frameworks > Library Imports > Local Imports


## Component
###JSX [TODO Reference js.md]
###Guidelines
###Common Usages
* useState: Hook used to store component state. (See: [useState Documentation](https://reactjs.org/docs/hooks-state.html))
* useEffect: Hook used to handle lifecycle changes. (OnSetup, OnChange, onUpdate ect.) (See: [useEffect Documentation](https://reactjs.org/docs/hooks-effect.html))
###PropType

## Javascript/Functionality
* 

## Styling [TODO Reference css.md]
* 

##TODO
* How to order imports..



