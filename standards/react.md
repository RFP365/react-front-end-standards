# React/JSX Style Guide (Forked AirBnB)

*A mostly reasonable approach to React and JSX*

This style guide is mostly based on the standards that are currently prevalent in JavaScript, although some conventions (i.e async/await or static class fields) may still be included or prohibited on a case-by-case basis. Currently, anything prior to stage 3 is not included nor recommended in this guide.

Note: This guide is meant to be a jumping off point. It barely encapsulates many of the concerns surrounding react.

## Table of Contents

1. [Naming](#naming)
1. [Alignment](#alignment)
1. [Quotes](#quotes)
1. [Spacing](#spacing)
1. [Props](#props)
1. [Refs](#refs)
1. [Parentheses](#parentheses)
1. [Tags](#tags)
1. [Methods](#methods)

## Basic Rules

- Only include one React component per file.
    - However, multiple [Stateless, or Pure, Components](https://facebook.github.io/react/docs/reusable-components.html#stateless-functions) are allowed per file. eslint: [`react/no-multi-comp`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/no-multi-comp.md#ignorestateless).
- Always use JSX syntax.
- Do not use `React.createElement` unless you’re initializing the app from a file that is not JSX.
- [`react/forbid-prop-types`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/forbid-prop-types.md) will allow `arrays` and `objects` only if it is explicitly noted what `array` and `object` contains, using `arrayOf`, `objectOf`, or `shape`.

## Naming

- **Filename**: Use PascalCase for filenames. E.g., `ReservationCard.js`.
- **Reference Naming**: Use PascalCase for React components and camelCase for their instances. eslint: [`react/jsx-pascal-case`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-pascal-case.md)

  ```jsx
  // bad
  import reservationCard from './ReservationCard';

  // good
  import ReservationCard from './ReservationCard';

  // bad
  const ReservationItem = <ReservationCard />;

  // good
  const reservationItem = <ReservationCard />;
  ```

- **Component Naming**: Use the filename as the component name. For example, `ReservationCard.js` should have a reference name of `ReservationCard`. However, for root components of a directory, use `index.js` as the filename and use the directory name as the component name:

  ```jsx
  // bad
  import Footer from './Footer/Footer';

  // bad
  import Footer from './Footer/index';

  // good
  import Footer from './Footer';
  ```

- **Higher-order Component Naming**: Use a composite of the higher-order component’s name and the passed-in component’s name as the `displayName` on the generated component. For example, the higher-order component `withFoo()`, when passed a component `Bar` should produce a component with a `displayName` of `withFoo(Bar)`.

  > Why? A component’s `displayName` may be used by developer tools or in error messages, and having a value that clearly expresses this relationship helps people understand what is happening.

  ```jsx
  // bad
  export default function withFoo(WrappedComponent) {
    return function WithFoo(props) {
      return <WrappedComponent {...props} foo />;
    }
  }

  // good
  export default function withFoo(WrappedComponent) {
    function WithFoo(props) {
      return <WrappedComponent {...props} foo />;
    }

    const wrappedComponentName = WrappedComponent.displayName
      || WrappedComponent.name
      || 'Component';

    WithFoo.displayName = `withFoo(${wrappedComponentName})`;
    return WithFoo;
  }
  ```

- **Props Naming**: Avoid using DOM component prop names for different purposes.

  > Why? People expect props like `style` and `className` to mean one specific thing. Varying this API for a subset of your app makes the code less readable and less maintainable, and may cause bugs.

  ```jsx
  // bad
  <MyComponent style="fancy" />

  // bad
  <MyComponent className="fancy" />

  // good
  <MyComponent variant="fancy" />
  ```

## Alignment

- Follow these alignment styles for JSX syntax. eslint: [`react/jsx-closing-bracket-location`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-closing-bracket-location.md) [`react/jsx-closing-tag-location`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-closing-tag-location.md)

  ```jsx
  // bad
  <Foo superLongParam="bar"
       anotherSuperLongParam="baz" />

  // good
  <Foo
    superLongParam="bar"
    anotherSuperLongParam="baz"
  />

  // if props fit in one line then keep it on the same line
  <Foo bar="bar" />

  // children get indented normally
  <Foo
    superLongParam="bar"
    anotherSuperLongParam="baz"
  >
    <Quux />
  </Foo>

  // bad
  {showButton &&
    <Button />
  }

  // bad
  {
    showButton &&
      <Button />
  }

  // good
  {showButton && (
    <Button />
  )}

  // good
  {showButton && <Button />}

  // good
  {someReallyLongConditional
    && anotherLongConditional
    && (
      <Foo
        superLongParam="bar"
        anotherSuperLongParam="baz"
      />
    )
  }

  // good
  {someConditional ? (
    <Foo />
  ) : (
    <Foo
      superLongParam="bar"
      anotherSuperLongParam="baz"
    />
  )}
  ```

## Quotes

- Always use double quotes (`"`) for JSX attributes, but single quotes (`'`) for all other JS. eslint: [`jsx-quotes`](https://eslint.org/docs/rules/jsx-quotes)

  > Why? Regular HTML attributes also typically use double quotes instead of single, so JSX attributes mirror this convention.

  ```jsx
  // bad
  <Foo bar='bar' />

  // good
  <Foo bar="bar" />

  // bad
  <Foo style={{ left: "20px" }} />

  // good
  <Foo style={{ left: '20px' }} />
  ```

## Spacing

- Always include a single space in your self-closing tag. eslint: [`no-multi-spaces`](https://eslint.org/docs/rules/no-multi-spaces), [`react/jsx-tag-spacing`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-tag-spacing.md)

  ```jsx
  // bad
  <Foo/>

  // very bad
  <Foo                 />

  // bad
  <Foo
   />

  // good
  <Foo />
  ```

- Do not pad JSX curly braces with spaces. eslint: [`react/jsx-curly-spacing`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-curly-spacing.md)

  ```jsx
  // bad
  <Foo bar={ baz } />

  // good
  <Foo bar={baz} />
  ```

## Props

- Always use camelCase for prop names, or PascalCase if the prop value is a React component.

  ```jsx
  // bad
  <Foo
    UserName="hello"
    phone_number={12345678}
  />

  // good
  <Foo
    userName="hello"
    phoneNumber={12345678}
    Component={SomeComponent}
  />
  ```

- Omit the value of the prop when it is explicitly `true`. eslint: [`react/jsx-boolean-value`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-boolean-value.md)

  ```jsx
  // bad
  <Foo
    hidden={true}
  />

  // good
  <Foo
    hidden
  />

  // good
  <Foo hidden />
  ```

- Always include an `alt` prop on `<img>` tags. If the image is presentational, `alt` can be an empty string or the `<img>` must have `role="presentation"`. eslint: [`jsx-a11y/alt-text`](https://github.com/evcohen/eslint-plugin-jsx-a11y/blob/master/docs/rules/alt-text.md)

  ```jsx
  // bad
  <img src="hello.jpg" />

  // good
  <img src="hello.jpg" alt="Me waving hello" />

  // good
  <img src="hello.jpg" alt="" />

  // good
  <img src="hello.jpg" role="presentation" />
  ```

- Do not use words like "image", "photo", or "picture" in `<img>` `alt` props. eslint: [`jsx-a11y/img-redundant-alt`](https://github.com/evcohen/eslint-plugin-jsx-a11y/blob/master/docs/rules/img-redundant-alt.md)

  > Why? Screenreaders already announce `img` elements as images, so there is no need to include this information in the alt text.

  ```jsx
  // bad
  <img src="hello.jpg" alt="Picture of me waving hello" />

  // good
  <img src="hello.jpg" alt="Me waving hello" />
  ```

- Use only valid, non-abstract [ARIA roles](https://www.w3.org/TR/wai-aria/#usage_intro). eslint: [`jsx-a11y/aria-role`](https://github.com/evcohen/eslint-plugin-jsx-a11y/blob/master/docs/rules/aria-role.md)

  ```jsx
  // bad - not an ARIA role
  <div role="datepicker" />

  // bad - abstract ARIA role
  <div role="range" />

  // good
  <div role="button" />
  ```

- Do not use `accessKey` on elements. eslint: [`jsx-a11y/no-access-key`](https://github.com/evcohen/eslint-plugin-jsx-a11y/blob/master/docs/rules/no-access-key.md)

> Why? Inconsistencies between keyboard shortcuts and keyboard commands used by people using screenreaders and keyboards complicate accessibility.

  ```jsx
  // bad
  <div accessKey="h" />

  // good
  <div />
  ```

- Avoid using an array index as `key` prop, prefer a stable ID. eslint: [`react/no-array-index-key`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/no-array-index-key.md)

> Why? Not using a stable ID [is an anti-pattern](https://medium.com/@robinpokorny/index-as-a-key-is-an-anti-pattern-e0349aece318) because it can negatively impact performance and cause issues with component state.

We don’t recommend using indexes for keys if the order of items may change.

  ```jsx
  // bad
  {todos.map((todo, index) =>
    <Todo
      {...todo}
      key={index}
    />
  )}

  // good
  {todos.map(todo => (
    <Todo
      {...todo}
      key={todo.id}
    />
  ))}
  ```

- Always define explicit defaultProps for all non-required props.

> Why? propTypes are a form of documentation, and providing defaultProps means the reader of your code doesn’t have to assume as much. In addition, it can mean that your code can omit certain type checks.

  ```jsx
  // bad
  function SFC({ foo, bar, children }) {
    return <div>{foo}{bar}{children}</div>;
  }
  SFC.propTypes = {
    foo: PropTypes.number.isRequired,
    bar: PropTypes.string,
    children: PropTypes.node,
  };

  // good
  function SFC({ foo, bar, children }) {
    return <div>{foo}{bar}{children}</div>;
  }
  SFC.propTypes = {
    foo: PropTypes.number.isRequired,
    bar: PropTypes.string,
    children: PropTypes.node,
  };
  SFC.defaultProps = {
    bar: '',
    children: null,
  };
  ```

- Use spread props sparingly.
> Why? Otherwise you’re more likely to pass unnecessary props down to components. And for React v15.6.1 and older, you could [pass invalid HTML attributes to the DOM](https://reactjs.org/blog/2017/09/08/dom-attributes-in-react-16.html).

Exceptions:

- HOCs that proxy down props and hoist propTypes

  ```jsx
  function HOC(WrappedComponent) {
    return class Proxy extends React.Component {
      Proxy.propTypes = {
        text: PropTypes.string,
        isLoading: PropTypes.bool
      };

      render() {
        return <WrappedComponent {...this.props} />
      }
    }
  }
  ```

- Spreading objects with known, explicit props. This can be particularly useful when testing React components with Mocha’s beforeEach construct.

  ```jsx
  export default function Foo {
    const props = {
      text: '',
      isPublished: false
    }

    return (<div {...props} />);
  }
  ```

Notes for use:
Filter out unnecessary props when possible. Also, use [prop-types-exact](https://www.npmjs.com/package/prop-types-exact) to help prevent bugs.

  ```jsx
  // bad
  render() {
    const { irrelevantProp, ...relevantProps } = this.props;
    return <WrappedComponent {...this.props} />
  }

  // good
  render() {
    const { irrelevantProp, ...relevantProps } = this.props;
    return <WrappedComponent {...relevantProps} />
  }
  ```

## Refs

- Always use ref callbacks. eslint: [`react/no-string-refs`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/no-string-refs.md)

  ```jsx
  // bad
  <Foo
    ref="myRef"
  />

  // good
  <Foo
    ref={(ref) => { this.myRef = ref; }}
  />
  ```

## Parentheses

- Wrap JSX tags in parentheses when they span more than one line. eslint: [`react/jsx-wrap-multilines`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-wrap-multilines.md)

  ```jsx
  // bad
  render() {
    return <MyComponent variant="long body" foo="bar">
             <MyChild />
           </MyComponent>;
  }

  // good
  render() {
    return (
      <MyComponent variant="long body" foo="bar">
        <MyChild />
      </MyComponent>
    );
  }

  // good, when single line
  render() {
    const body = <div>hello</div>;
    return <MyComponent>{body}</MyComponent>;
  }
  ```

## Tags

- Always self-close tags that have no children. eslint: [`react/self-closing-comp`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/self-closing-comp.md)

  ```jsx
  // bad
  <Foo variant="stuff"></Foo>

  // good
  <Foo variant="stuff" />
  ```

- If your component has multiline properties, close its tag on a new line. eslint: [`react/jsx-closing-bracket-location`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-closing-bracket-location.md)

  ```jsx
  // bad
  <Foo
    bar="bar"
    baz="baz" />

  // good
  <Foo
    bar="bar"
    baz="baz"
  />
  ```

## Methods

- Use arrow functions to close over local variables. It is handy when you need to pass additional data to an event handler. Although, make sure they [do not massively hurt performance](https://www.bignerdranch.com/blog/choosing-the-best-approach-for-react-event-handlers/), in particular when passed to custom components that might be PureComponents, because they will trigger a possibly needless rerender every time.

  ```jsx
  function ItemList(props) {
    return (
      <ul>
        {props.items.map((item, index) => (
          <Item
            key={item.key}
            onClick={(event) => { doSomethingWith(event, item.name, index); }}
          />
        ))}
      </ul>
    );
  }
  ```

- Be sure to return a value in your `render` methods. eslint: [`react/require-render-return`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/require-render-return.md)

  ```jsx
  // bad
  render() {
    (<div />);
  }

  // good
  render() {
    return (<div />);
  }
 ```
