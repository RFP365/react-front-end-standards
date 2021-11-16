# Storybook Stories Example

`Storybook` is an open source tool for building UI components and pages in isolation. 
It streamlines UI development, testing, and documentation.

A story is defined alongside it's mocked component. 
Start with the smallest piece and create a story early (or first) to prototype it.
Work your way up to larger and larger components.

---

## Prototyping with Storybook in a nutshell.

1. Break off the smallest piece of UX/UI you are working on. Define the props it will take.
> Component:`exampleComponent.js` 
```jsx
/**
 * @param prop1
 * @param prop2
 */
export const ExampleComponent = ({prop1, prop2}) => {
    return (
        <StyledExampleComponent></StyledExampleComponent>
    );
};

ExampleComponent.propTypes = {};
```


2. Define a story file alongside of it.
> Story:`exampleComponent.stories.js`

```jsx
/**
 * Define a Component and Title. argTypes expose helpful testing controls in Storybook.
 * Create templates and attach args or define standalone stories.
 */
export default {
    component: ExampleComponent,
    title: 'Example Component',
    argTypes: {
        rangeOrNumPropName: {
            control: {type: 'range', min: 0, max: 100, step: 2},
        },
        textPropName: {
            control: {type: 'text'}
        },
        selectPropName: {
            control: {
                type: 'select',
                options: {
                    Small: 'small',
                    Medium: 'medium',
                },
            },
        },
        onClick: { action: 'chip clicked' }, //ClickHandler
        onDelete: { action: 'chip deleted' }, //DeleteHandler
    }
}

/**
 * Template Method
 * 1. Create one or multiple "core" templates.
 * 2. Bind a Story and then add testing args to it.
 */
const ExampleComponentTemplate = (args) => <ExampleComponent {...args} />;
export const exampleComponent = ExampleComponentTemplate.bind({});
exampleComponent.args = {
    rangeOrNumPropName: 70,
    textPropName: 'Loading...'
}

const SecondExampleTemplate = (args) => <SecondExample {...args} />;
export const secondExample = SecondExampleTemplate.bind({});
secondExample.args = {
    rangeOrNumPropName: 0,
    textPropName: ''
}

/**
 * Alternative way to define "example" standalone stories.
 */
export const WithAvatar = () => (
    <StyledRoot>
        <ExampleChip label="Now with Avatar" color="primary" avatar={<Avatar>M</Avatar>} />
    </StyledRoot>
);
```

3. To run the `storybook` instance for a library/App
````
nx storybook {project-name}
````
4. Now you can prototype/test your component in isolation through it's functional props.

### Storybook Setup Note
To generate the config and add storybook support to a new Nx App/Lib.
This will create a `.storybook` directory in the project with the required setup for storybook.
````
nx g storybook-configuration --project {project-name}
````


## Mocking an Endpoint
If your component uses a service hook and needs to mock and endpoint for prototyping or testing, we utilize `Mock Service Worker`(msw). 
>Mock by intercepting requests on the network level. Seamlessly reuse the same mock definition for testing, development, and debugging.

###Creating a Mock
Open the `libs/test-utils/src/lib/mocks/handlers.js` file. In this file, there is an exported `const handler` array which has entries that mock rest endpoints like this:

```js
export const handlers = [
  // ... other handlers
  rest.get('/account/active-company', (req, res, ctx) => {
    return res(ctx.status(200), ctx.json(complexCompany));
  }),
  // ... other handlers
];
```

Each of the entries provides a mock response for the configured endpoint. When storybook is ran and a component makes a request to this endpoint, the given response is returned.
To add another mocked endpoint, add an entry with the given HTTP verb (GET, POST, etc), and provide it the data you would like returned.

Note: Add the mock lib(common-util) to `nx.json` > `implicitDependencies` for your lib.
You will also need to register the mocks to start up in your `.storybook/preview.js`
```js
if (typeof global.process === 'undefined') {
    const {worker} = require('../../test-utils/src/lib/mocks');
    worker.start();
}
```

## Additional Resources
* [Storybook Based development tutorial](https://storybook.js.org/tutorials/intro-to-storybook/react/en/get-started/)
* [Writing Stories Documentation](https://storybook.js.org/docs/react/writing-stories/introduction)
* [Mock Service Worker Documentation/Examples](https://mswjs.io/examples/)
* See `rfp360-web` > `common-ui` stories for further examples.
