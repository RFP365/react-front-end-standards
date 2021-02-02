# File &amp; Folder Structure

##Folder Structure

Here is an example of an Nx Component Lib.

    . feature-one
    ├── common                          # [PascalCase].js
    ├── components                      
    |   ├── FirstComponent.js           
    |   ├── FirstComponent.spec.js      
    |   ├── FirstComponent.stories.js
    ├── constants                       # [PascalCase].js 
    |   ├── docType.constant.js   
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


##Folders [snake-case]
### common
* Re-usable common-ui components.
* Candidates to elevate to global `libs > common-ui`.
### components(TODO LINK TO COMPONENT EXAMPLE File)
* Components used by the feature.
* Broken out by feature > sub-components. 
### constants
* Feature specific constants.
* Candidates to elevate to global `libs > models`.
### containers
* Generally provide a data-retrieval layer to make root components more functional.
* [Tutorial on Containers](https://scotch.io/courses/5-essential-react-concepts-to-know-before-learning-redux/presentational-and-container-component-pattern-in-react)
### contexts
* Context files hold feature state via React Context.
* [Documentation on Contexts]((https://reactjs.org/docs/context.html))
### services
* Service files hold logic related to API calls.
* Candidates to elevate to global `libs > common-services`.
### utils
* Util files such as `*.hooks.js` & `*.utils.js` house state hooks and component util functions.
* Candidates to elevate to global `libs > common-util`.

## Naming Conventions
###C omponents [PascalCase]
 Ex: `Component.js`, `ComponentContext.js`, `ComponentContainer.js`
### Folder Names [snake-case]
Ex: `components`, `feature-one`, `feature-one-sub-component`
### Everything Else [barrel.case]
Ex: `account.service.js`, `getUser.hooks.js`, `userItems.utils.js`

## Questions to Answer
* Do Context and Container need their own folder. Could we combine them?
* Do we want to make some file names consistent? .utils.js vs camelCase.
* Should we make hooks separate or slide it in to utils?
* Some of our naming conventions are mixed. Do we want to stake down on these three?
