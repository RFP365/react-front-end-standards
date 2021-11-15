# Storybook Stories Example

Storybook is an open source tool for building UI components and pages in isolation. 
It streamlines UI development, testing, and documentation.

A story is defined alongside it's mocked component. 
Start with the smallest piece and create a story early (or first) to prototype it.
Work your way up to larger and larger components.
---

> Component:`exampleComponent.js` / Story:`exampleComponent.stories.js`

```jsx
/**
 * Define a Component and Title. argTypes expose helpful testing controls in Storybook.
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

To generate the config and add storybook support to a new Nx App/Lib.
This will create a `.storybook` directory in the project with the required setup for storybook.
````
nx g storybook-configuration --project {project-name}
````

To run the `storybook` instance for a library/App
````
nx storybook {project-name}
````

## Additional Resources
* [Storybook Based development tutorial](https://storybook.js.org/tutorials/intro-to-storybook/react/en/get-started/)
* [Writing Stories Documentation](https://storybook.js.org/docs/react/writing-stories/introduction)
* See `rfp360-web` > `common-ui` stories for further examples.
