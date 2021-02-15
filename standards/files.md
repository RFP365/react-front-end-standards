# File &amp; Folder Structure Guidelines

Here is an example of an Nx Component Lib.

---

    . feature-one
    ├── common                          # [PascalCase].js
    ├── components                      
    |   ├── FirstComponent.js           
    |   ├── FirstComponent.spec.js      
    |   ├── FirstComponent.stories.js
    ├── constants                       # [object].[constant].js
    |   ├── docType.constant.js
    ├── prop-types                      # [object].[propTypeShape].js
    |   ├── customer.propTypeShape.js   
    ├── containers                      # [PascalCase].js 
    |   ├── MainComponentContainer.js   
    ├── contexts                        # [PascalCase].js   
    |   ├── FeatureContext.js
    ├── services                        # [object].service.js
    |   ├── firstComponent.service.js   
    ├── utils                           # [object].[type].js
    |   ├── camelCaseComponent.utils.js                
    |   ├── hookMethod.hooks.js 
    └── index.js                         # Export file.


## Folders [kebab-case]
### common
* Re-usable common-ui components.
* Candidates to elevate to global `libs > common-ui`.
### components (See: [Component Example](../examples/component.md))
* Components used by the feature.
* Broken out by feature > sub-components. 
### constants (See: [Constant Example](../examples/constant.md))
* Feature specific constants.
* Candidates to elevate to global `libs > models > constants`.
### prop-types (See: [Shape Example](../examples/shape.md))
* Feature specific PropTypeShapes.
* Candidates to elevate to global `libs > models > prop-types`.
### containers
* Generally provide a data-retrieval layer to promote more functional design.
* [Tutorial on Containers](https://scotch.io/courses/5-essential-react-concepts-to-know-before-learning-redux/presentational-and-container-component-pattern-in-react)
### contexts (See: [Context Example](../examples/context.md))
* Context files hold feature state via React Context.
* [Documentation on Contexts]((https://reactjs.org/docs/context.html))
### services (See: [Service Example](../examples/service.md))
* Service files hold logic related to API calls.
* Candidates to elevate to global `libs > common-services`.
### utils (See: [Hook Example](../examples/hook.md))
* Util files such as `*.hooks.js` & `*.utils.js` house state hooks and component util functions.
* Candidates to elevate to global `libs > common-util`.

## Naming Conventions
### Components [PascalCase]
 Ex: `Component.js`, `ComponentContext.js`, `ComponentContainer.js`
### Stories/Tests [ComponentName.centric.case]
 Ex: `OverviewMode.spec.js`, `BigButton.stories.js`
### Folder Names [kebab-case]
Ex: `components`, `feature-one`, `feature-one-sub-component`
### Everything Else [domain-area.centric.case]
Ex: `account.service.js`, `get-user.hooks.js`, `user-items.utils.js`

## Questions to Answer
* Do Context and Container need their own folder. Could we combine them?
* Do we want to make some file names consistent? .utils.js vs camelCase.
* Should we make hooks separate or slide it in to utils?
* Some of our naming conventions are mixed. Do we want to stake down on these three?
