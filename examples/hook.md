# Hook Example

Hooks are used to expose custom functionality within functional components.
This is often the correct way to expose `*.service.js` or `*.utils.js` methods.
---

````jsx
import {useState} from 'react';

import {storeItem, retrieveItem, evictItem} from './storage.service';

/**
 * Wrap the storage.service logic in a custom hook to interact with the storage
 * @param {string} key the key to store/retrieve the item in the cache from
 * @param {string | unknown} [initialValue = null] an initial value to use if the item is null
 * @returns {Object} the item, handleSetItem fn, and handleEvictItem fn
 */
export const useStorage = (key, initialValue = null) => {
    const [item, setItem] = useState(() => {
        const itemFromStorage = retrieveItem(key);
        return itemFromStorage ?? initialValue;
    });

    const handleSetItem = (itemToSet) => {
        setItem(itemToSet);
        storeItem(key, itemToSet);
    };

    const handleEvictItem = () => {
        setItem(null);
        evictItem(key);
    };

    return {item, handleSetItem, handleEvictItem};
};
````

## Additional References
* [Building your own hooks](https://reactjs.org/docs/hooks-custom.html)
