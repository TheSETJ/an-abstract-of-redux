# An abstract of Redux

This document is a very simple abstract of Redux which written based on the official documentation and mainly with React in mind.

## [Store](https://redux.js.org/basics/store)

**Store** is the only source of truth of the app and is created using [`createStore()`](https://redux.js.org/api/createstore). It does the following:
- holds state
- allows access to state using [`getState()`](https://redux.js.org/api/store#dispatch-action)
- allows state being updated via [`dispatch()`](https://redux.js.org/api/store#dispatch-action)
- register listeners via [`subscribe()`](https://redux.js.org/api/store#dispatch-action)
- handles unregistering of listeners

## [Actions](https://redux.js.org/basics/actions)

**Actions** are the only source of information for the Store. They are JavaScript object:
```javascript
{
  // it's a string and is required
  type: 'ANY_ACTION_TYPE',
  // the information and is optional
  payload: {}
}
```
Action should be dispatched using [`dispatch()`](https://redux.js.org/api/store#dispatch-action).

## [Reducers](https://redux.js.org/basics/reducers)

**Reducers** define initial state of the app and each new state of the app using previous state and an action.

`(previousState, action) => newState`

Reducers can be separated if they are independent and can be merged using [`combineReducers()`](https://redux.js.org/api/combinereducers).


## Simple steps to add Redux to the app

1. Create your initial state and reducer(s):
```javascript
const initialState = { /* initial values */ }
const anyReducer = (state = initialState, action) => {
  switch(action.type) {
    /* cases */
    default:
      return state;
  }
};
```
2. Create store and provide it with merged reducer:
```javascript
import { createStore } from 'react';

// the only source of truth
const store = createStore(anyReducer /* or combined reducer in case of having more than one */);
```
3. Provide app with store:
```js
import { Provider } from 'react-redux';

// surround highest level component of the app with <Provider>
render() {
  return (
    <Provider store={store}>
      <App />
    </Provider>
  );
}
```
4. Connect components to redux and provide [`connect()`](https://github.com/reduxjs/react-redux/blob/master/docs/api.md#connectmapstatetoprops-mapdispatchtoprops-mergeprops-options) with at least a function which maps state to props:
```javascript
const anyMapStateToProps = (state) => {
  return {
    /* map each property inside state argument to a property of this object */
  };
};

// export the result of connect()
// not evey component needs to be connected
export default connect(anyMapStateToProps)(myComponent)
```
5. Dispatch actions whenever needed:
```javascript
// anywhere that needs a change of state
// dispatch can be found in the props of the component
this.props.dispatch({ type: 'ANY_ACTION_TYPE', /* pass required info, if any */ })
```

## [Useful Resources](#useful-resources)
- https://redux.js.org/
- https://github.com/reduxjs/redux
- https://github.com/reduxjs/react-redux
- https://www.youtube.com/watch?v=sX3KeP7v7Kg
- https://www.youtube.com/watch?v=93p3LxR9xfM
