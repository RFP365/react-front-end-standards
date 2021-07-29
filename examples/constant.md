# Simple React Constant Example

Below is a simple react constant definition file. Naming convention. Use these to increase cohesion throughout the app and reduce duplication errors. 

---
> `product-type.constants.js`

```js
export const ProductType = Object.freeze({
    ISSUING: 'ISSUING',
    RESPONDING: 'RESPONDING',
    KNOWLEDGE: 'KNOWLEDGE',
});
```

## Usage
```jsx
const getTheme = (productType) => {
  switch (productType) {
    case ProductType.RESPONDING:
      return respondingTheme;
    case ProductType.ISSUING:
      return issuingTheme;
    default:
      return respondingTheme;
  }
};
```
