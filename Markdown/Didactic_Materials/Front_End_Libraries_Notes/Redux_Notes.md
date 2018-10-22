# Redux Notes
 
### Create a Redux Store
In Redux, there is a single state object housed in the Redux store that is responsible for the state of the entire app. This state must be updated any time the app needs to update state. This causes a unidirectional flow.
```javascript
const reducer = (state = 5) => {
  return state;
}
//Above is the reducer, which takes an argument of state and returns state
const store = Redux.createStore(reducer);
//This is the Redux store, which uses the method createStore() which passes the reducer as an argument
```
A more concise way to create the store would be:
```javascript
const store = Redux.createStore(
  (state = 5) => state
);
```
### Get State from the Redux Store
Use the method getState() to retrieve the current state.

```javascript
const store = Redux.createStore(
  (state = 5) => state
); //the store is created
const currentState = store.getState();
//the current state is retrieved
```
### Define a Redux Action
An "action" is a JavaScript object that contains information about an action event that has occured.  Redux actions must have a "type" and are used to update the state in the Redux store.  Think of them as messengers carrying info or evnt data to the Redux store.
Here is an example:
```javascript 
const action = {
  type: 'LOGIN'
}
```
### Define an Action Creator
Now that we've created a Redux action, it needs to be sent to the Redux store.  In order to do this, we need to create a Redux action creator.  An action creator is just a JavaScript function that returns an action.
e.g.
```javascript
function actionCreator() {
  return action;
}
```
### Dispatch an Action Event
The dispatch method is used to send the action to the Redux store.  To dispatch "LOGIN," from the previous example, one could use either of these dispatch methods.
```javascript
store.dispatch(actionCreator());
store.dispatch({ type: 'LOGIN' });
```
In the example below, the dispatch code that follows dispatches the login info to the store:

```javascript
store.dispatch(loginAction());
```
Here is the full example:
```javascript
const store = Redux.createStore(
  (state = {login: false}) => state
);

const loginAction = () => {
  return {
    type: 'LOGIN'
  }
};

store.dispatch(loginAction());
```
### Handle an Action in the Store
The reducer function is responsible for modifying the state in response to a Redux action.  Because the state in Redux is read-only, the reducer creates a new state and never modifies the state directly.

This example shows how the state will be modified in response to an action:
```javascript
const defaultState = {
  login: false
};

const reducer = (state = defaultState, action) => {
  return action.type == 'LOGIN' ? {login: true} : defaultState;
  // This ternary operator returns a new state if the loginAction.type is 'LOGIN' and the same state if not.
};

const store = Redux.createStore(reducer);

const loginAction = () => {
  return {
    type: 'LOGIN'
  }
};
```
### Use a Switch Statement to Handle Multiple Actions
This example uses a switch statement to update the state based on possible actions.
```javascript
const defaultState = {
  authenticated: false
};

const authReducer = (state = defaultState, action) => {
  switch (action.type) {
    default:
    return {authenticated: false};
    case 'LOGIN':
    return {authenticated: true};
    case 'LOGOUT':
    return {authenticated: false};
  }
  /** The switch statement handles three cases: 
   * 1) By default, it will set authenticated to false. 
   * 2) If loginUser is dispatched, it will set it to true. 
   * 3) If logoutUser is called, it will set it to false.
   */
};

const store = Redux.createStore(authReducer);

const loginUser = () => {
  return {
    type: 'LOGIN'
  }
};

const logoutUser = () => {
  return {
    type: 'LOGOUT'
  }
};
```
### Use const for Action Types
To bolster security and prevent unwanted changes, the action types are made into read-only const variables.  See example below:
```javascript
const LOGIN = 'LOGIN';
const LOGOUT = 'LOGOUT';
// The values of the potential state values are now read-only constants

const defaultState = {
  authenticated: false
};

const authReducer = (state = defaultState, action) => {

  switch (action.type) {

    case LOGIN: //This is a const variable
      return {
        authenticated: true
      }

    case LOGOUT: //This is a const variable
      return {
        authenticated: false
      }

    default:
      return state;

  }

};

const store = Redux.createStore(authReducer);

const loginUser = () => {
  return {
    type: LOGIN // This is a const variable
  }
};

const logoutUser = () => {
  return {
    type: LOGOUT //This is a const variable
  }
};
```
### Register a Store Listener
The method store.subscribe() is a listener function which is called any time an action is dispatched to the store.  
This example will add to a counter every time the listener function hears an action being dispatched to the store.
```javascript
const ADD = 'ADD';

const reducer = (state = 0, action) => {
  switch(action.type) {
    case ADD:
      return state + 1;
    default:
      return state;
  }
};

const store = Redux.createStore(reducer);

let count = 0;
const addToCount = () => count +=1;
store.subscribe(addToCount);
/** The function addToCount is adding 1 to the count.
 * store.subscribe() will pass addToCount as a callback every time an action is dispatched to the store
 */

store.dispatch({type: ADD});
console.log(count);
store.dispatch({type: ADD});
console.log(count);
store.dispatch({type: ADD});
console.log(count);
//The count will now be 3
```
### Combine Multiple Reducers
Because there is only one store that holds the state(s) in Redux, if one wishes to make more than one state and keep track of them easily, one can make more than one reducer instead of multiple stores. These reducers are then combined with the combineReducers() method so the Redux store state(s) can be modified by one over-arching root reducer function.
```javascript
const INCREMENT = 'INCREMENT';
const DECREMENT = 'DECREMENT';

const counterReducer = (state = 0, action) => {
  switch(action.type) {
    case INCREMENT:
      return state + 1;
    case DECREMENT:
      return state - 1;
    default:
      return state;
  }
};

const LOGIN = 'LOGIN';
const LOGOUT = 'LOGOUT';

const authReducer = (state = {authenticated: false}, action) => {
  switch(action.type) {
    case LOGIN:
      return {
        authenticated: true
      }
    case LOGOUT:
      return {
        authenticated: false
      }
    default:
      return state;
  }
};

const rootReducer = 
  Redux.combineReducers({
    count: counterReducer,
    auth: authReducer
  });
  //The reducers are combined into a rootReducer
  
const store = Redux.createStore(rootReducer);
//The rootReducer is passed to createStore instead of the individual reducers.
```
### Send Action Data to the Store
Instead of sending a type to the store with a dispatch, this example sends data. This is useful if the state will be updated based on user input.
The example below will updat the state to whatever data is passed into the function addNoteText.
```javascript
const ADD_NOTE = 'ADD_NOTE';

const notesReducer = (state = 'Initial State', action) => {
  switch(action.type) {
    // change code below this line
    case ADD_NOTE:
    return action.text;
    // If ADD_NOTE is the action.type, the data stored in addNoteText.text will be returned.
    default:
      return state;
  }
};

const addNoteText = (note) => {
    return {
      type: ADD_NOTE,
      text: note
    };
  // The input that is passed into the function will be addNoteText.text
};

const store = Redux.createStore(notesReducer);

console.log(store.getState());
store.dispatch(addNoteText('Hello!'));
console.log(store.getState());
```
### Use Middleware to Handle Asynchronous Actions
Redux has special Redux Thunk Middleware to handle asynchronous actions.  To include this middleware, add Redux.applyMiddleware() as a second argument to the createStore() method. To create an asynchronous action, return a function in the action creator that takes dispatch as an argument.  It is common to dispatch an action before initiating asynchronous behavior so the app state knows that data is being requested.  After the data is received, another action carries the data along with info that the action is complete. The example below passes a dispatch, requestingData(), followed by a mock API setTimeout, followed by another dispatch, receivedData().  The middleware processes the asynchronous action.
```javascript
const REQUESTING_DATA = 'REQUESTING_DATA'
const RECEIVED_DATA = 'RECEIVED_DATA'

const requestingData = () => { return {type: REQUESTING_DATA} }
const receivedData = (data) => { return {type: RECEIVED_DATA, users: data.users} }

const handleAsync = () => {
  return function(dispatch) {
     dispatch(requestingData());  // dispaching requestData
    setTimeout(function() {
      let data = {
        users: ['Jeff', 'William', 'Alice']
      }
      dispatch(receivedData(data)); //dispatching received Data

    }, 2500);
  }
};

const defaultState = {
  fetching: false,
  users: []
};

const asyncDataReducer = (state = defaultState, action) => {
  switch(action.type) {
    case REQUESTING_DATA:
      return {
        fetching: true,
        users: []
      }
    case RECEIVED_DATA:
      return {
        fetching: false,
        users: action.users
      }
    default:
      return state;
  }
};

const store = Redux.createStore(
  asyncDataReducer,
  Redux.applyMiddleware(ReduxThunk.default)
);
```
### Write a Counter with Redux
This is a simple Redux counter.
```javascript
const INCREMENT = 'INCREMENT'
const DECREMENT = 'DECREMENT'

const counterReducer = (state = 0, action) => {
switch(action.type){
  default:
  return state;
  case INCREMENT:
  return state + 1;
  case DECREMENT:
  return state -1;
}
}

const incAction = () => {
  return {
    type: INCREMENT
  }
}
const decAction = () => {
  return {
    type: DECREMENT 
  }
}

const store = Redux.createStore(counterReducer);
```
### Never Mutate State
The Redux store's state should never be mutated. Instead, a read-only version of each state-change should be saved and a new state should replace the former.  Unfortunatley, Redux doesn't supply any protection against this: it's the responsibility of the coder.
The data type matters in terms of mutability: a string or number are immutable by nature, however an array or object are mutable and measures must be taken to ensure the state isn't mutated if the type is array or object.

The example below updates the store w/o mutating the state using concat, i.e.
```javascript
switch(action.type) {
    case ADD_TO_DO:
      return state.concat(action.todo);
```
This or several other measures taken from ideas of functional programming can be used to ensure the state is not mutated.
Here's the full example:

```javascript
const ADD_TO_DO = 'ADD_TO_DO';

// A list of strings representing tasks to do:
const todos = [
  'Go to the store',
  'Clean the house',
  'Cook dinner',
  'Learn to code',
];
//The reducer can't mutate the state
const immutableReducer = (state = todos, action) => {
  switch(action.type) {
    case ADD_TO_DO:
      return state.concat(action.todo);
    default:
      return state;
  }
};

const addToDo = (todo) => {
  return {
    type: ADD_TO_DO,
    todo
  }
}

const store = Redux.createStore(immutableReducer);
```
### Use the Spread Operator on Arrays
Another way to complete the task above is to make a copy of the state and add the new data with the spread operator.  See example:
```javascript
const immutableReducer = (state = ['Do not mutate state!'], action) => {
  switch(action.type) {
    case 'ADD_TO_DO':
      return [...state, action.todo];
      //The former state is copied w/o being mutated and the new items are added.
    default:
      return state;
  }
};

const addToDo = (todo) => {
  return {
    type: 'ADD_TO_DO',
    todo
  }
}

const store = Redux.createStore(immutableReducer);
```
### Remove an Item from an Array
The goal of this example is to remove an item from the state array w/o mutating the actual state:
```javascript
const immutableReducer = (state = [0,1,2,3,4,5], action) => {
  switch(action.type) {
    case 'REMOVE_ITEM':
      return [...state.slice(0,action.index),...state.slice(action.index+1)];
      /**This takes a spread copy of the state up to (but not including)
       * and after the action.index 
       * without mutating the original state*/  
    default:
      return state;
  }
};

const removeItem = (index) => {
  return {
    type: 'REMOVE_ITEM',
    index
  }
}

const store = Redux.createStore(immutableReducer);
```
### Copy an Object with Object.assign
Object.assign copies properties from one or more source objects and overwrites values from the argument that have the same keys as the source and adds new key:value pairs if the source doesn't include the new property.

For instance, 
```javascript
let obj = { a: 10 };
let copy = Object.assign({}, obj);
console.log(copy); // { a: 10 }
//obj is the source object and it has been copied into the blank object in hte first argument of Object.assign
``` 
Object.assign() will merge properties from the arguments from right to left.  So, for this example, we update the state object so the status changes to 'online' when action.type is 'ONLINE.'  In order to do so, we use this switch statement:
```javascript
switch(action.type) {
    case 'ONLINE':
    return Object.assign({}, state, {status: 'online'})
```
The changed property, status, will merge and overwrite the state object, which will be merged into an empty object.  This makes a copy of the state object with desired changes w/o mutating the original state.  

Here is the full example:
```javascript
const defaultState = {
  user: 'CamperBot',
  status: 'offline',
  friends: '732,982',
  community: 'freeCodeCamp'
};

const immutableReducer = (state = defaultState, action) => {
  switch(action.type) {
    case 'ONLINE':
      return Object.assign({}, state, {status: 'online'})
    default:
      return state;
  }
};

const wakeUp = () => {
  return {
    type: 'ONLINE'
  }
};

const store = Redux.createStore(immutableReducer);
```

For more details on Object.assign, <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/assign" target=blank>click here</a>

