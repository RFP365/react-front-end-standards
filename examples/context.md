# ContextExample

Context is primarily used when some data needs to be accessible by many components at different nesting levels. 
Apply it sparingly because it makes component re-use more difficult.

````jsx
import React, {createContext, useContext, useState, useEffect, useRef} from 'react';

import {ProductType} from '@rfp360-web/models';
import {storeItem, retrieveItem} from '@rfp360-web/common-services';

export const defaultAppContext = {
    product: ProductType.RESPONDING,
    setProduct: undefined,
    isSidenavOpen: false,
    setSidenavOpen: undefined,
};

const AppContext = createContext(defaultAppContext);
const useApp = () => useContext(AppContext);

/**
 * Build a component wrapper around the {AppContext}.
 * Creates a default state for the context for use in the app
 * @param {Object} AppProviderProps
 * @param {React.ReactNode} AppProviderProps.children component children to wrap with the app context
 * @returns {React.FC}
 */
const AppProvider = ({children}) => {
    const [product, setProduct] = useState(ProductType.RESPONDING);
    const [isSidenavOpen, setSidenavOpen] = useState(true);

    return (
        <AppContext.Provider
            value={{
                product,
                setProduct,
                isSidenavOpen,
                setSidenavOpen,
            }}
        >
            {children}
        </AppContext.Provider>
    );
};

export {AppContext, useApp, AppProvider};
````

Then wrap the component in a Context.Provider
````jsx
<AppProvider>
    <YourComponent/>
</AppProvider>
````

You can use the hook `useContext` or wrap it within your context to access it.
````jsx
const {product, setProduct, isSidenavOpen, setSidenavOpen} = useApp();
````

## Additional Resources
* [Building your own Context](https://reactjs.org/docs/context.html)
