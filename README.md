# An abstract of Redux

This document is a very simple abstract of Redux which written based on the official documentation and 2 other videos, and mainly with React in mind. You can find them in [Useful Resources](#useful-resources) section.

## [Store](https://redux.js.org/basics/store)

**Store** is the only source of truth of the app and is created using `createStore()`. It does the following:
- holds state
- allows access to state using `getState()`
- allows state being updated via `dispatch()`
- register listeners via `subscribe()`
- handles unregistering of listeners

## [Actions](https://redux.js.org/basics/actions)

**Actions** are the only source of information for the Store. They are JavaScript object:
```javascript
{
  type: it's a string and is required
  payload: the information
}
```
Action should be dispatched using `dispatch()`.

## [Reducers](https://redux.js.org/basics/reducers)

**Reducers** define initial state of the app and each new state of the app using previous state and an action.

`(previousState, action) => newState`

Reducers can be separated if they are independent and can be merged using `combineReducers()`.


## Simple steps to add Redux to the app

1. Create your initial state and reducer(s):
```javascript
const initialState = { /* whatever */ }
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
const store = createStore(/* reducer */);
```
3. Provide app with store:
```jsx
<Provider store={store}>
  /* app components */
</Provider>
```
4. Connect components to redux and provide connector with a state-to-props-mapper:
```javascript
const anyMapStateToProps = (state) => {
  return {
    /* map each property inside state argument to a property of this object */
  };
};
```
5. Dispatch actions whenever needed:
```javascript
/* anywhere need a change of state */
this.props.dispatch({ type: 'ANY_ACTION_TYPE', /* pass required info, if any */ })
```

## [Useful Resources](#useful-resources)
- https://redux.js.org/
- https://www.youtube.com/watch?v=sX3KeP7v7Kg
- https://www.youtube.com/watch?v=93p3LxR9xfM
