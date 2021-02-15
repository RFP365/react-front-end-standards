# PropType Shape Example

Shape objects are used to document and abstract large, complicated, or commonly used propType sets. Named `[object].propTypeShape.js`

---

```jsx
import PropTypes from 'prop-types';

export const companyPropTypesShape = {
  eId: PropTypes.string.isRequired,
  clientId: PropTypes.string.isRequired,
  name: PropTypes.string.isRequired,
  displayName: PropTypes.string,
  path: PropTypes.string,
  status: PropTypes.oneOf(['ACTIVE', 'INACTIVE', 'DELETED']).isRequired,
  isActiveInHierarchy: PropTypes.bool.isRequired,
  accountOwner: PropTypes.object,
  subCompanies: PropTypes.array,
};
```

## Usage
Use in PropTypes for other components
```jsx
UsesCompanyProp.propTypes = {
    companyHierarchy: PropTypes.shape(companyPropTypesShape).isRequired,
    handleStopImpersonation: PropTypes.func.isRequired,
};
```
