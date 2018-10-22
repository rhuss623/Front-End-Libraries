# React and Redux Notes
Hi! My name is Ryan Hussey and these are my personal notes for freeCodeCamp's React and Redux lessons.  Full disclosure - much of the example code comes directly from freeCodeCamp - I'm not trying to plagiarize, these are just my notes for keeping track of what I've learned. Feel free to use them.

### Manage State Locally First
This example isn't using Redux, it's just a React app that is managing the state locally
```javascript
class DisplayMessages extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      input: '',
      messages: []
    }
    //State initiates w/ empty string input and empty array for messages
    this.handleChange = this.handleChange.bind(this);
    this.submitMessage = 
    this.submitMessage.bind(this);
    //Binding this to handleChange and submitMessage
  }
  
  handleChange(event){
    this.setState({
      input: event.target.value
    })
  }
  //An event in handleChange will change the state to the value of the input
  submitMessage(event){
    event.preventDefault;
    //this prevents the default state from being submitted
    this.setState({
      input: "", //this clears the input
      messages: [...this.state.messages, this.state.input] //this copies the former messages and adds the new input w/o mutating the original state
    });                   
  }
                                               
  render() {
    const list = this.state.messages.map(a => <li>{a}</li>); 
    //This variable maps the messages array and puts values into an li
    return (
      <div>
        <h2>Type in a new Message:</h2>
          <input type="text" value={this.state.input} onChange={this.handleChange.bind(this)} />{/* handleChange is called when a change happens in the input */}
          <button type="submit" onClick={this.submitMessage}>Submit!</button>
          <ul>{list}</ul>
        </div>
    );
  }
};
```
### Extract State Logic to Redux
We need to connect the React app from above to the Redux store. Here, we create a Redux store and give it a reducer and action creator that update the store state.  See comments in example:
```javascript
const ADD = 'ADD';//This will be used as the type for addMessage, declaring it as a const makes it read-only

function addMessage(newMessage){
  return {
    type: ADD,
    message: newMessage
  };
};
//This is a Redux action creator, passing a newMessage into addMessage.message

const messageReducer = (state, action)=> {
    return [...state, action.message]//This will add addMessage.message to the state w/o mutating state
};
//This is the reducer, responsible for making changes to the state

const store = {
state: [],
getState: () => store.state,
dispatch: (action) => {
  if (action.type === ADD) {
    store.state = messageReducer(store.state, action)
  }
//This will update the state using the reducer if addMessage is dispatched
}
};
```
<br><br>
This works, as well, and is more concise:
<br><br><br>
```javascript
const ADD = 'ADD';

const addMessage = (message) => {
  return {
    type: ADD,
    message
  }
};

const messageReducer = (state = [], action) => {
  switch (action.type) {
    case ADD:
      return [
        ...state,
        action.message
      ];
    default:
      return state;
  }
};

const store = Redux.createStore(messageReducer);
```
### Use Provider to Connect Redux to React
Now we need to connect React to the Redux store and give it the tools necessary to dispatch updates to the store state.  We will use the React Redux API features "Provider" and "connect."  This challenge only covers Provider, a later challenge uses connect.  Provider is a wrapper for your React app that allows the React app to dispatch to the Redux store.  Provider takes two props:
* The Redux store
and
* The child components of the React app
An example of defining Provider looks like this:
```javascript
 <Provider store={store}>
  <App/>
</Provider>
```
The Redux and React examples used previously are combined, with the addition of this code to render the Provider:
```javascript
const Provider = ReactRedux.Provider;

class AppWrapper extends React.Component {
   render() {
       return (
    <Provider store={store}>
    <DisplayMessages/>
    </Provider>
    )}
};
```
Here is the full example:

```javascript
// Redux Code:
const ADD = 'ADD';

const addMessage = (message) => {
  return {
    type: ADD,
    message
  }
};

const messageReducer = (state = [], action) => {
  switch (action.type) {
    case ADD:
      return [
        ...state,
        action.message
      ];
    default:
      return state;
  }
};



const store = Redux.createStore(messageReducer);

// React Code:

class DisplayMessages extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      input: '',
      messages: []
    }
    this.handleChange = this.handleChange.bind(this);
    this.submitMessage = this.submitMessage.bind(this);
  }
  handleChange(event) {
    this.setState({
      input: event.target.value
    });
  }
  submitMessage() {
    const currentMessage = this.state.input;
    this.setState({
      input: '',
      messages: this.state.messages.concat(currentMessage)
    });
  }
  render() {
    return (
      <div>
        <h2>Type in a new Message:</h2>
        <input
          value={this.state.input}
          onChange={this.handleChange}/><br/>
        <button onClick={this.submitMessage}>Submit</button>
        <ul>
          {this.state.messages.map( (message, idx) => {
              return (
                 <li key={idx}>{message}</li>
              )
            })
          }
        </ul>
      </div>
    );
  }
};

const Provider = ReactRedux.Provider;

class AppWrapper extends React.Component {
  // The Provider is rendered:
   render() {
       return (
    <Provider store={store}>
    <DisplayMessages/>
    </Provider>
    )}
   
};
```
### Map State to Props
You can use mapStateToProps() and mapDispatchToProps() to use the Provider to provide dispatch and state to React components. In these functions, you declare what pieces of state you want to have access to and which action creators you need to be able to dispatch. 
This example shows a state (which consists of a single property) being passed with mapStateToProps.
```javascript
const state = [];
function mapStateToProps(state) {
return {
    messages: state
}
}
```
### Map Dispatch to Props
mapDispatchToProps() provides specific action creators to React components so they can dispatch to the Redux store. 

Here's an example from freeCodeCamp:
"For example, you have a loginUser() action creator that takes a username as an action payload. The object returned from mapDispatchToProps() for this action creator would look something like:"
```javascript
{
  submitLoginUser: function(username) {
    dispatch(loginUser(username));
  }
}
```
The example below has an action creator, addMessage(), which is dispatched w/ mapDispatchToProps():

```javascript
const addMessage = (message) => {
  return {
    type: 'ADD',
    message: message
  }
};

function mapDispatchToProps(dispatch) {
    return {
        submitNewMessage: function(newMessage) {
            dispatch(addMessage(newMessage))
        }
    }
}
```
### Connect Redux to React
To connect the dispatches and state between React and Redux, use connect() w/ mapDispatchToProps() and/or mapStateToProps() as arguments. 
```javascript
connect(mapStateToProps, mapDispatchToProps)(MyComponent)
```
To omit one of these arguments, pass null in its place.  Notice the order of the arguments.
Here is the part of the following example that connects the React component to the Redux store:
```javascript
const connect = ReactRedux.connect;

const ConnectedComponent = connect( mapStateToProps, mapDispatchToProps)(Presentational);
```
And here is the full example:
```javascript
const addMessage = (message) => {
  return {
    type: 'ADD',
    message: message
  }
};

const mapStateToProps = (state) => {
  return {
    messages: state
  }
};

const mapDispatchToProps = (dispatch) => {
  return {
    submitNewMessage: (message) => {
      dispatch(addMessage(message));
    }
  }
};

class Presentational extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return <h3>This is a Presentational Component</h3>
  }
};

const connect = ReactRedux.connect;

const ConnectedComponent = connect(mapStateToProps, mapDispatchToProps)(Presentational);
```
### Connect Redux to the Messages App
Quoted from freeCodeCamp:
"In the last lesson, the component you connected to Redux was named Presentational, and this wasn't arbitrary. This term generally refers to React components that are not directly connected to Redux. They are simply responsible for the presentation of UI and do this as a function of the props they receive. By contrast, container components are connected to Redux. These are typically responsible for dispatching actions to the store and often pass store state to child components as props."

This example makes the connection and has the Provider, see comments:
```javascript
// Redux:
const ADD = 'ADD';

const addMessage = (message) => {
  return {
    type: ADD,
    message: message
  }
};

const messageReducer = (state = [], action) => {
  switch (action.type) {
    case ADD:
      return [
        ...state,
        action.message
      ];
    default:
      return state;
  }
};

const store = Redux.createStore(messageReducer);

// React:
class Presentational extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      input: '',
      messages: []
    }
    this.handleChange = this.handleChange.bind(this);
    this.submitMessage = this.submitMessage.bind(this);
  }
  handleChange(event) {
    this.setState({
      input: event.target.value
    });
  }
  submitMessage() {
    const currentMessage = this.state.input;
    this.setState({
      input: '',
      messages: this.state.messages.concat(currentMessage)
    });
  }
  render() {
    return (
      <div>
        <h2>Type in a new Message:</h2>
        <input
          value={this.state.input}
          onChange={this.handleChange}/><br/>
        <button onClick={this.submitMessage}>Submit</button>
        <ul>
          {this.state.messages.map( (message, idx) => {
              return (
                 <li key={idx}>{message}</li>
              )
            })
          }
        </ul>
      </div>
    );
  }
};

// React-Redux:
const mapStateToProps = (state) => {
  return { messages: state }
};

const mapDispatchToProps = (dispatch) => {
  return {
    submitNewMessage: (newMessage) => {
       dispatch(addMessage(newMessage))
    }
  }
};

const Provider = ReactRedux.Provider;
const connect = ReactRedux.connect;

const Container = connect(mapStateToProps, mapDispatchToProps)(Presentational);
//The React to Redux connection is made

class AppWrapper extends React.Component {
  render() {
    return (
      <Provider store={store}>
        <Container/>
      </Provider>
    );
  }
};
//The Provider w/ prop store is rendered w/ Container as child prop
```
### Extract Local State into Redux
There is still local state management in the previous example, so that management needs to be put into Redux.

The changes made in the example below have removed the property "message."  The message prop is now solely controlled by the redux store.

```javascript
// Redux:
const ADD = 'ADD';

const addMessage = (message) => {
  return {
    type: ADD,
    message: message
  }
};

const messageReducer = (state = [], action) => {
  switch (action.type) {
    case ADD:
      return [
        ...state,
        action.message
      ];
    default:
      return state;
  }
};

const store = Redux.createStore(messageReducer);

// React:
const Provider = ReactRedux.Provider;
const connect = ReactRedux.connect;

// Change code below this line
class Presentational extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      input: ''
      //messages has been removed from the local state
    }
    this.handleChange = this.handleChange.bind(this);
    this.submitMessage = this.submitMessage.bind(this);
  }
  handleChange(event) {
    this.setState({
      input: event.target.value
    });
  }
  submitMessage() {
    this.props.submitNewMessage(this.state.input)
    this.setState({
      input: ''
      //messages has been removed from the local state
    });
  }
  render() {
    return (
      <div>
        <h2>Type in a new Message:</h2>
        <input
          value={this.state.input}
          onChange={this.handleChange}/><br/>
        <button onClick={this.submitMessage}>Submit</button>
        <ul>
          {this.props.messages.map( (message, idx) => {
              return (
                 <li key={idx}>{message}</li>
              )
            })
          }
        </ul>
      </div>
    );
  }
};

const mapStateToProps = (state) => {
  return {messages: state}
};

const mapDispatchToProps = (dispatch) => {
  return {
    submitNewMessage: (message) => {
      dispatch(addMessage(message))
    }
  }
};

const Container = connect(mapStateToProps, mapDispatchToProps)(Presentational);

class AppWrapper extends React.Component {
  render() {
    return (
      <Provider store={store}>
        <Container/>
      </Provider>
    );
  }
};
```
### Moving Forward From Here
Copied and pasted from freeCodeCamp:
"Congratulations! You finished the lessons on React and Redux. There's one last item worth pointing out before you move on. Typically, you won't write React apps in a code editor like this. This challenge gives you a glimpse of what the syntax looks like if you're working with npm and a file system on your own machine. The code should look similar, except for the use of import statements (these pull in all of the dependencies that have been provided for you in the challenges). The "Managing Packages with npm" section covers npm in more detail.

Finally, writing React and Redux code generally requires some configuration. This can get complicated quickly. If you are interested in experimenting on your own machine, the

<a href="https://github.com/facebook/create-react-app" target=blank>Create React App</a> comes configured and ready to go.

Alternatively, you can enable Babel as a JavaScript Preprocessor in CodePen, add React and ReactDOM as external JavaScript resources, and work there as well.
" <br>
The sample code that they are referring to (code w/ imports, etc. that were already configured behind the scenes in freeCodeCamp) are here:
```javascript
 import React from 'react'
 import ReactDOM from 'react-dom'
 import { Provider, connect } from 'react-redux'
 import { createStore, combineReducers, applyMiddleware } from 'redux'
 import thunk from 'redux-thunk'

 import rootReducer from './redux/reducers'
 import App from './components/App'

 const store = createStore(
   rootReducer,
   applyMiddleware(thunk)
 );

 ReactDOM.render(
   <Provider store={store}>
     <App/>
   </Provider>,
   document.getElementById('root')
 );

```

