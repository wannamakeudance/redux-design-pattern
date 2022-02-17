### 0. Create a function named CreateStore which returns a null object 

```javascript
const createStore = reducer => {
    return {
      
    };
};
```

### 1.Add interfaces such as store.getState/store.dispatch/store.subscribe to this object 

```javascript
const createStore = (reducer, initValue) => {
    const getState = () => {};
    const dispatch = () => {};
    const subscribe = () => {};
    return {
        getState,
        dispatch,
        subscribe
    };
};
```

### 2. Realize the getState interface

```javascript
const createStore = (reducer = () => {}, initValue = {}) => {
    let _store = initValue;
    const getState = () => {
        return _store;
    };
    ...
};
```


### 2. Realize the dispatch interface

```javascript
const createStore = (reducer = () => {}, initValue = {}) => {
    let _store = initValue;
    ...
    const dispatch = action => {
        // Change the _store through reducer function which you define outside the whole createStore
        _store = reducer(_store, action);
    };
    ...
};
```

### 3. Realize the subscribe interface

```javascript
const createStore = (reducer = () => {}, initValue = {}) => {
    let _store = initValue;
    let _storeListeners = [];
    ...

    const dispatch = action => {
        _store = reducer(_store, action);
        // When dispatch an action, the listener function will execute.
        _storeListeners.forEach(listener => {
            listener();
        });
    };

    const subscribe = listener => {
        _storeListeners.push(listener);
    };
    ...
};
```
----------
*You can refer to this [whole code](./src/2.md).*