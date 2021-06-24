# NX Guidelines

Nx is a versatile tool that helps with things such as:

- Code organization and ownership
- Developer workflow
- Deployment flexibility

These guidelines are based off of their best practices and general use cases, as well as some of our own design decisions.

[Nx at Enterprises](https://nx.dev/latest/angular/guides/monorepo-nx-enterprise)
[Nx Libraries](https://nx.dev/latest/angular/structure/library-types)

## Apps

Apps handle dependency injection and wire up libraries. They should only ever contain high level components that are specific to the use case for that app specifically. Apps shouldn't import heavily from other Nx libraries - feature libraries should ideally build out a single component that will be brought into an application.

`apps > feature libraries > component libraries & utility libraries`

## Libs

Libs (Libraries) contain services, components, and utilities that have a well-defined public API. As our app grows and more legacy code is converted over, the number of libs we have will grow as well. It is important to pay attention to the organization of the libs directory to maintain a clean codebase.

Libraries with a broader scope (such as shared UI components) should not depend on libraries with a narrower scope (such as a specific feature).

Component libraries should only ever depend on other component libraries and utility libraries, and should not depend on feature libraries. If there is a component you find you would re-use in another feature library, try to move it out into a common one. Down the line, we can enforce this sort of rule using [tags](https://nx.dev/latest/react/structure/monorepo-tags).

## Library Types

### UI Libraries

These libraries should contain only presentational components, which should have high reusability. Any data they need should come from inputs or parent feature components, and never any sort of services.

#### **Naming Convention**

`*-ui` or `ui-\*` if nested

#### **Dependency Constraints**

A UI Library can depend on UI and Utility libraries

---

### Feature Libraries

Feature Libraries contain a set of files that configure a business use case or a page in an application. Most components will be smart ocmponents that interact with data sources. Feature Libraries are almost always going to be app-specific and are often lazy-loaded.

When creating a feature library, try to include a `README.md` file outlining the folder structure. 

#### **Naming Convention**

`feature` or `feature-home` if nested

#### **Dependency Constraints**

A feature library can depend on any type of library.

#### **Feature Library File Structure**

```
|- feature/
| |- src/
|   |- lib/
|     |- feature-home/
|       |- components/                    <- houses smaller feature components
|         |- components-sub-domain/       <- multiple sub-domains if necessary, e.g. Section vs Workflow etc
|       |- feature.js                     <- primary component to export
|       |- feature.stories.js
|       |- feature.spec.js
|       |- featureContext.js              <- context file for the feature component
|       |- render.js                      <- if the primary feature component is being used as an entry-point
|       |- index.js                       <- barrel file exporting out the primary feature component
|     |- index.js                         <- barrel file exporting out all feature components
|   |- index.js                           <- barrel file exporting out all lib exports. this is what is available to import from this module
```

---

### Utility Libraries

Utility libraries contain low level code used by many libraries. Often there is no framework-specific code and the library is simply a collection of utilities or pure functions.

#### **Naming Convention**

`*-util` 

#### **Dependency Constraints**

Utility libraries should only depend on utility libraries.

---

## Using Code from Nx Libraries

Generally speaking, any publicly accessed functions should be exported directly, and never via default export. From there they should be exported out from a barrel file in their current directory, all the way up the file structure, eg:

```javascript
## library-name/src/lib/thing/service.js
// good
export const someFunction = () => {
     // implementation
}

// bad
export default someFunction = () => {
    // implementation
}
```

```javascript
## library-name/src/lib/thing/index.js
export * from './service.js';
```

```javascript
## library-name/src/lib/index.js
export * from './thing';
```

From here, other libraries will have access to anything exported out of `/lib/index.js` by destructuring the library import. Avoid importing from libraries by navigating through the file structure, as this results in dependency issues that can be tricky to track down.

```javascript
// good
import { someFunction } from '@rfp360-web/library-name';

// very bad why would you ever do this
import { someFunction } from '../../../../../../library-name/src/lib/thing/service.js';
```

## Import Order

Anytime we're building components, we'll want to disitinguish where we're importing from. We have three different sources, and they should imported in this order, spaced out:

Note: **Material UI imports should be imported directly and never destructured, per their docs.**

1. Dependencies and packages (usually from yarn)

2. `rfp360-web` libraries

3. Local files in the same general app/lib folder

```javascript
import React, { useEffect, useState } from 'react';
import { useQuery } from 'react-query';
import Grid from '@material-ui/core/Grid';

import { ErrorText, TruncatedText } from '@rfp360-web/common-ui';
import { someHook } from '@rfp360-web/common-services';

import { useFeatureContext } from './FeatureContext';
import { SomeSkeleton } from './components/SomeSkeleton';
```
