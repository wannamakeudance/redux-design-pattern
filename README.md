# This artile is to explain how to design a simple redux step by step.

### Step0. Create a function named CreateStore which has two parameters and returns a null object 

```javascript
const createStore = (reducer, initValue) => {
    return {
      
    };
};
```

### Step1.Add interfaces such as store.getState/store.dispatch/store.subscribe to this object 

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

### Step2. Realize the getState interface

```javascript
const createStore = (reducer = () => {}, initValue = {}) => {
    let _store = initValue;
    const getState = () => {
        return _store;
    };
    ...
};
```


### Step3. Realize the dispatch interface

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

### Step4. Realize the subscribe interface

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
### Step5. Realize the unsubscribe function

```javascript
const createStore = (reducer = () => {}, initValue = {}) => {
    ...
    
    const subscribe = listener => {
        _storeListeners.push(listener);
        // to unsubscribe this listener
        return () => {
            const index = _storeListeners.indexOf(listener);
            _storeListeners.splice(index, 1);
        }
    };
    ...
};
```

### Conclusion

In my opinion, the implementation of redux has involved two major design patterns: **Singleton Pattern and Observer Pattern.**
Furthermore, the whole unique store is the practice of `Software Closure`.

----------
## *You can refer to [this file](./src/2.md) with whole code.*