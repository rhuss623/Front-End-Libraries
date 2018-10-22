# React Notes
Hi! My name is Ryan Hussey and these are my personal notes for freeCodeCamp's React lessons.  Full disclosure - much of the example code comes directly from freeCodeCamp - I'm not trying to plagiarize, these are just my notes for keeping track of what I've learned. <br>Feel free to use them.

To write JavaScript directly w/ JSX, put the JavaScript inside curly braces 
```javascript
{...}
```
Note that JSX is not valid JavaScript(i.e. it's not an interpreted language), it needs to be compiled in order to run. Babel is a popular compiler for this purpose.

### Create a Simple JSX Element

```JavaScript
const JSX = <h1>Hello JSX!</h1>;
```
### Create a Complex JSX Element

To create a more complex element, make sure to give any sibling element a parent wrapper. 
e.g.

Correct:
```HTML
<div>
<p>Sibling 1</p>
<p>Sibling 2</p>
</div>
```

Incorrect:
```HTML
<p>Sibling 1</p>
<p>Sibling 2</p>
<!--Won't be transpiled correctly-->
```
Example:
```JavaScript
const JSX = ( 
<div>
<h1>Complex JSX</h1>
<p> React is so cool!!!</p>
</div>
    );
```

### Add Comments in JSX
To comment, use {/* */}
```JavaScript
 {/*Comment Here*/}
```

### Render HTML Elements
Using React, we can render the JSX to the HTML DOM using React's rendering API ReactDOM:
```JavaScript
ReactDOM.render(componentToRender, targetNode)
```
* First Argument: The element or component that you want to render.
* Second Argument: The DOM node that you are rendering to.
e.g.
```javascript
ReactDOM.render(JSX,document.getElementById('challenge-node'));
```
### Define an HTML Class in JSX
First, there is an important naming convention in JSX: All events and attributes are camelCase in JSX.

Second, when designating a class in JSX, use: <span style=color:red>className</span>.

```JavaScript
const JSX = (
  <div className= "myDiv">
    <h1>Classy</h1>
  </div>
);
```

### Learn About Self-Closing JSX Tags
To write a self-closing tag in JSX, such as <span style=color:red><br></span>, include a space and forward slash at the end of the tag. e.g.
```JavaScript
const JSX = (
<div>
    <p>Words</p>
    <br />
    <p>More Words</p>
</div>
);
```

### Create a Stateless Functional Component
To create a React component w/ a function, make a JavaScript function that returns either JSX or <span style=color:red>null</span>.
e.g.
```JavaScript
const MyComponent = function() {
return (
<div>
<p>Text</p>
</div>
);
};
```
This is a stateless function.
### Create a React Component
Another way to create a React component is w/ ES6 <span style=color:red>class</span> syntax.

```javascript

class MyComponent extends //the new class MyComponent extends the React.Component class.
React.Component {
  constructor(props) { //MyComponent is a constructor
    super(props); //MyComponent calls the constructor of the parent class w/ super()
  }
  render() {
    return (
<div>
<h1>Hello React!</h1>
</div>
  );
  }
};
```
### Create a Component with Composition
You can use multiple components w/in one component and they will display in the order they are rendered. e.g.

```JavaScript
const ChildComponent = () => {
  return (
    <div>
      <p>I am the child</p>
    </div>
  );
};

class ParentComponent extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
      <div>
        <h1>I am the parent</h1>
        <ChildComponent /> 
      </div>
    );
  }
```
Notice that the ChildComponent tag is self-closing.
### Use React to Render Nested Components
Here, we've nested a component, TypesOfFruit, w/in a second component, Fruits and rendered both in TypesOfFood by rendering Fruits.
```javascript
const TypesOfFruit = () => {
  return (
    <div>
      <h2>Fruits:</h2>
      <ul>
        <li>Apples</li>
        <li>Blueberries</li>
        <li>Strawberries</li>
        <li>Bananas</li>
      </ul>
    </div>
  );
};

const Fruits = () => {
  return (
    <div>
   <TypesOfFruit />
    </div>
  );
};

class TypesOfFood extends React.Component {
  constructor(props) {
    super(props);
  }

  render() {
    return (
      <div>
        <h1>Types of Food:</h1>
        <Fruits />
      </div>
    );
  }
};
```
### Render a Class Component to the DOM
To render a class component to the DOM, use closing brackets for the component you are trying to render, e.g. <span style=color:red>ReactDOM.render(<ComponentToRender />, targetNode)</span>.
e.g.
```JavaScript
ReactDOM.render(<TypesOfFood />,document.getElementById('challenge-node'));
```
### Pass Props to a Stateless Functional Component
To pass a property into a stateless function, see the example below:
```JavaScript
const CurrentDate = (props) => {
  return (
    <div>
      <p>The current date is: {props.date} </p> {/* Property of date is set */}
    </div>
  );
};

class Calendar extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
      <div>
        <h3>What date is it?</h3>
        <CurrentDate date={Date()}/> {/* The JavaScript Date object is used to supply todays date */}
      </div>
    );
  }
};
```
The property, date, is set in CurrentDate and the property, which doesn't have a value assigned, yet, is assigned the value {Date()}, which is a JavaScript object that will return todays date.

### Pass an Array as Props
To pass an array as props, use curly braces, as above.  When accessing the array, array methods can be used, such as <span style=color:red>.join()</span>.  e.g.
```javascript
const List= (props) => {
  return <p>{props.tasks.join(", ")}</p> {/*The property of tasks is set and the array will be joined w/ ", " */}
};

class ToDo extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
      <div>
        <h1>To Do Lists</h1>
        <h2>Today</h2>
        <List tasks= {["Learn React", "Learn Meisner Technique"]}/> {/* The tasks property has values assigned */}
        <h2>Tomorrow</h2>
        <List tasks = {["Review React and Meisner","now you can react in film and on a computer", "react on all the screens!"]}/>
        { /* change code above this line */ }
      </div>
    );
  }
};
```
### Use Default Props
To assign a default value to a property, see the example:
```JavaScript
const ShoppingCart = (props) => {
  return (
    <div>
      <h1>Shopping Cart Component</h1>
    </div>
  )
};

ShoppingCart.defaultProps = {quantity: 0}
```
### Override Default Props
To override the default value for the quantity property of Items, below, simply designate a new value while rendering. e.g.
```JavaScript
const Items = (props) => {
  return <h1>Current Quantity of Items in Cart: {props.quantity}</h1>
}

Items.defaultProps = {
  quantity: 0
}

class ShoppingCart extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return <Items quantity={10}/>
  }
};
```
### Use PropTypes to Define the Props You Expect
To ensure the correct type of data is being rendered, you can check the property type w/ propTypes.

Some types are
* string
* number
* array
* object
* func (for function)
* bool (for boolean)
* any  (for any type)

In order to use propTypes, it must be imported independently of React, using:
<span style=color:red>import React, { PropTypes } from 'react';</span>

Here's an example of a number type being required for the quantity property of Item:
```JavaScript
const Items = (props) => {
  return <h1>Current Quantity of Items in Cart: {props.quantity}</h1>
};
Items.propTypes = {
  quantity: PropTypes.number.isRequired
}
```
### Access Props Using this.props
To access props w/in an ES6 class component, use <span style=color:red>this</span>, e.g.:
```javascript   
class ReturnTempPassword extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
        <div>
            <p>Your temporary password is: <strong>{this.props.tempPassword}</strong></p> {/* The prop tempPassword is set using this */}
        </div>
    );
  }
};

class ResetPassword extends React.Component {
  constructor(props) {
    super(props);

  }
  render() {
    return (
        <div>
          <h2>Reset Password</h2>
          <h3>We've generated a new temporary password for you.</h3>
          <h3>Please reset this password from your account settings ASAP.</h3>
        <ReturnTempPassword tempPassword={"bestPasswordEver"} />{/* The prop tempPassword is assigned a value */}
        </div>
    );
  }
};
```
### Quick Review of State vs Stateless
First, a few definitions:
* Stateless functional component:
    *Any function which accepts props and returns JSX
* Stateless component:
    * Class that extends React.component, but doesn't use internal state
* Stateful component (aka components or React components):
    * Maintains its internal state 

### Create a Stateful Component
Declare the state of the component w/ <span style=color:red>this.state = {...state declaration, here}</span>.
The state can be altered by declaring a new assignment when rendering in other components.  Here's an example of a state being declared and called:
```javascript

class StatefulComponent extends React.Component {
  constructor(props) {
    super(props);
  this.state = {
    name : "name"
  }
  {/*The State is declared*/}
                      
  }
  render() {
    return (
      <div>
        <h1>{this.state.name}</h1> 
            {/*The State is called*/}
      </div>
    );
  }
};
```
### Render State in the User Interface

Here's what freeCodeCamp says in this lesson: 
"Once you define a component's initial state, you can display any part of it in the UI that is rendered. If a component is stateful, it will always have access to the data in state in its render() method. You can access the data with this.state.

If you want to access a state value within the return of the render method, you have to enclose the value in curly braces.

State is one of the most powerful features of components in React. It allows you to track important data in your app and render a UI in response to changes in this data. If your data changes, your UI will change. React uses what is called a virtual DOM, to keep track of changes behind the scenes. When state data updates, it triggers a re-render of the components using that data - including child components that received the data as a prop. React updates the actual DOM, but only where necessary. This means you don't have to worry about changing the DOM. You simply declare what the UI should look like.

Note that if you make a component stateful, no other components are aware of its state. Its state is completely encapsulated, or local to that component, unless you pass state data to a child component as props. This notion of encapsulated state is very important because it allows you to write certain logic, then have that logic contained and isolated in one place in your code."

### Render State in the User Interface Another Way
It is also possible to set a variable to the state and call that variable later, as below:
```javascript
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      name: 'freeCodeCamp'
    }
  }
  render() {

  const name = this.state.name 
    // The variable is set to the state
    return (
      <div>
      <h1>{name}</h1>
        { /* The variable is called */ }
      </div>
    );
  }
};
```

### Set State with this.setState
Never modify the state directly.  One way to modify state is to use <span style=color:red>this.setState()</span>.
e.g.
```javascript
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      name: 'Initial State'
    };
    this.handleClick = this.handleClick.bind(this);
  }
  handleClick() {
  this.setState({
    name: 'React Rocks!'
  });
   //the state is changed w/ handleClick()
  }
  render() {
    return (
      <div>
        <button onClick={this.handleClick}>Click Me</button>
        <h1>{this.state.name}</h1>
      </div>
    );
  }
};
```

### Bind 'this' to a Class Method
In the example above, the handleClick method uses <span style=color:red>this.handleClick = this.handleClick.bind(this);</span> so that, when <span style=color:red>this.setState</span> is invoked, the <span style=color:red>this</span> will be defined by the class.

For a brief explanation on 'this,' see <a href = "https://www.youtube.com/watch?v=zE9iro4r918" target=blank>this video</a>.

### Use State to Toggle an Element
The if/else statement below is toggling the state of visibility by changing the state to true or false.
```javascript
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      visibility: false
    };
this.toggleVisibility = this.toggleVisibility.bind(this);
  }
    toggleVisibility() {
      if (this.state.visibility==true) {
      this.setState({
    visibility: false
  });
      }
      else {
        this.setState({
          visibility: true
        })
      };
    }
  render() {
    if (this.state.visibility) {
      return (
        <div>
          <button onClick={this.toggleVisibility}>Click Me</button>
          <h1>Now you see me!</h1>
        </div>
      );
    } else {
      return (
        <div>
          <button onClick={this.toggleVisibility}>Click Me</button>
        </div>
      );
    }
  }
};
```
### Write a Simple Counter
Below is a counter with methods increment, decrement and reset.

```javascript
class Counter extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      count: 0
    };
    
    this.increment = this.increment.bind(this);
   this.decrement = this.decrement.bind(this);
   this.reset = this.reset.bind(this);
  }
    increment() {
      this.setState({
        count : this.state.count + 1
      })
    };
    decrement() {
      this.setState ({
        count : this.state.count - 1
      })
    };
    reset() {
      this.setState ({
        count: 0
      })
    }
  
  render() {
    return (
      <div>
        <button className='inc' onClick={this.increment}>Increment!</button>
        <button className='dec' onClick={this.decrement}>Decrement!</button>
        <button className='reset' onClick={this.reset}>Reset</button>
        <h1>Current Count: {this.state.count}</h1>
      </div>
    );
  }
};
```
### Create a Controlled Input
A Controlled Input will store values in the state, which is localized and therefore won't have interactions with other code.  This is beneficial for security.  See the comments in the example for details.
 ```javascript
class ControlledInput extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      input: ''
    };
    this.handleChange = this.handleChange.bind(this);
  }
handleChange(event) {
      this.setState({
        input: event.target.value //handleChange changes the state
      }) 
    }
  render() {
    return (
      <div>
      <input type = "text" value = {this.state.input} onChange = {this.handleChange.bind(this)}/>
{/* Above, the input value is set to store its value in submit, making it controlled. */}
        <h4>Controlled Input:</h4>
        <p>{this.state.input}</p>
      </div>
    );
  }
};
```
<a href="https://www.youtube.com/watch?v=BvtQMxekmH0" target=blank>Here's a video explaining how to create a controlled form.</a>

### Create a Controlled Form
See above for short explanation of controlling inputs/forms. See comments on example below for more details.
```javascript
class MyForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      input: '',
      submit: ''
    };
    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }
  handleChange(event) {
    this.setState({
      input: event.target.value
    });
  }
  handleSubmit(event) {
    event.preventDefault();//This prevents the default setting from being submitted.
  this.setState({
    input: '', 
    submit: this.state.input //This sets the state of submit to the input value;
  });
  }
  render() {
    return (
      <div>
        <form onSubmit={this.handleSubmit}>

        <input value={this.state.input} onChange={this.handleChange}/>
        {/* Above, the input value is set to store its value in submit, making it controlled. */}
          <button type='submit'>Submit!</button>
        </form>
      <h1>{this.state.submit}</h1>
      </div>
    );
  }
};
```
### Pass State as Props to Child Components
It is beneficial to have a stateful parent element that passes limited state props to children.  This limits access to the state properties to the places it's actually needed.  The example below shows two important ideas in React.  Whenever possible, one should code their React with the following:
* The information-flow is unidirectional: from the parent to the child via the state.
* There is only one stateful function, thus separating the app into a stateful component and UI rendering component(s).

```JAVASCRIPT
class MyApp extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      name: 'CamperBot'
    }
  }
  render() {
    return (
       <div>
         <Navbar name={this.state.name} /> 
        //Here, the Navbar gains the property name from the state.
       </div>
    );
  }
};

class Navbar extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
    <div>
      <h1>Hello, my name is:{this.props.name} </h1>
        //Because Navbar already has access to name property, above, it will render that property here. 
    </div>
    );
  }
};
```
### Pass a Callback as Props
As above, the information in this example is passed from the stateful component to the UI rendering component(s) as props.

```JAVASCRIPT
class MyApp extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      inputValue: ''
    }
    this.handleChange = this.handleChange.bind(this);
  }
  handleChange(event) {
    this.setState({
      inputValue: event.target.value
    });
  }
  render() {
    return (
       <div>
      <GetInput input={this.state.input} handleChange={this.handleChange} />
      <RenderInput input={this.state.inputValue} />   
            //The handler and input both get their properties from the state.
       </div>
    );
  }
};

class GetInput extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
      <div>
        <h3>Get Input:</h3>
        <input
          value={this.props.input}
          onChange={this.props.handleChange}/>
            //The state values can be passed as props in both
      </div>
    );
  }
};

class RenderInput extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
      <div>
        <h3>Input Render:</h3>
        <p>{this.props.input}</p>
      </div>
    );
  }
};
```
### Use the Lifecycle Method componentWillMount

React components have special lifecycle methods (aka lifecycle hooks) that allow one to call an action at a specific moment.  The lifecycle can be broken down into four stages: Initialization >> Mounting >> Updating >> Unmounting.  Here are some commonly used lifecycle hooks:

* componentWillMount()

* componentDidMount()

* componentWillReceiveProps()   

* shouldComponentUpdate()

* componentWillUpdate()

* componentDidUpdate() 
* componentWillUnmount()

    The example below simply shows a componentWillMount method.
    ```JavaScript
    
    class MyComponent extends React.Component {
  constructor(props) {
    super(props);
  }
                                               
  componentWillMount() {
  console.log("willMount")
  } //componentWillMount is before render
                                               
  render() {
    return <div />
  }
};
```

### Use the Lifecycle Method componentDidMount
When calling an API endpoint to retrieve data, it is usually best to do so w/in the componentDidMount method.
This example uses a mock API.
```JAVASCRIPT
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      activeUsers: null
    };
  }
  componentDidMount() {
    setTimeout( () => {
      this.setState({
        activeUsers: 1273
      });
    }, 2500);
  }
  render() {
    return (
      <div>
        <h1>Active Users: { this.state.activeUsers }</h1>
      </div>
    );
  }
};
```
### Add Event Listeners
An event listener is useful because it provides a synthetic event system that acts independently of the native event system, so it will behave the same despite the native browswer event systems.  
The example below has an event listener document.addEventListener() in the componentDidMount() method, which receives a first argument of an event and a second argument of a callback.  This event listener is removed in the componentWillMount() method.  Removing an event listener before the component is unmounted or destroyed is a good practice.
```JAVASCRIPT
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      message: ''
    };
    this.handleEnter = this.handleEnter.bind(this);
    this.handleKeyPress = this.handleKeyPress.bind(this);
  }
  componentDidMount() {
    document.addEventListener("keydown", this.handleKeyPress) //When the keydown event happens, handleKeyPress method will be enacted.
  }
  componentWillUnmount() {
    document.removeEventListener("keydown", this.handleKeyPress) //Before the component, handleKeyPress, unmounts, the event listener is removed
  }
  handleEnter() {
    this.setState({
      message: this.state.message + 'You pressed the enter key! '
    });
  }
  handleKeyPress(event) {
    if (event.keyCode === 13) {
      this.handleEnter();
    }
  }
  render() {
    return (
      <div>
        <h1>{this.state.message}</h1>
      </div>
    );
  }
};
```

### Manage Updates with Lifecycle Methods
For the Updating stage of the lifecycle, the example below will deal with these progressions of the update:
componentWillReceiveProps >> componentWillUpdate >> componentDidUpdate.

This is what is happening in each method in the example function, below:

componentWillReceiveProps is checking to see if new props are receieved.  If so, w/in the method we will compare the new and old props, with NextProps being the new and this.props being the old.  In this example, it's simply logging both the old and new props.

componentWillUpdate occurs before rendering and checks to see if there have been any state or props updates.  In our function, it will simply log "Component is about to update."

After rendering, componentDidUpdate is logging "Component has updated."

```JAVASCRIPT
class Dialog extends React.Component {
  constructor(props) {
    super(props);
  }
  componentWillReceiveProps(nextProps) {
    console.log(this.props, nextProps)
  }
  componentWillUpdate() {
    console.log('Component is about to update...');
  }
  componentDidUpdate() {
    console.log("Component has updated.")
  }
  render() {
    return <h1>{this.props.message}</h1>
  }
};

class Controller extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      message: 'First Message'
    };
    this.changeMessage = this.changeMessage.bind(this);
  }
  changeMessage() {
    this.setState({
      message: 'Second Message'
    });
  }
  render() {
    return (
      <div>
        <button onClick={this.changeMessage}>Update</button>
        <Dialog message={this.state.message}/>
      </div>
    );
  }
};
```
### Optimize Re-Renders with shouldComponentUpdate
shouldComponentUpdate takes nextProps and nextState as parameters.  This is used to determine whether the components should update when a new state or prop are recieved.  One use is to make sure that re-rendering doesn't occur if the new prop is the same as the old prop.

The example below uses shouldComponentUpdate to re-render if the nextProps value is even.

```javascript
class OnlyEvens extends React.Component {
  constructor(props) {
    super(props);
  }
  shouldComponentUpdate(nextProps, nextState) {
    console.log('Should I update?');
    return (nextProps.value % 2 == 0) ? true : false  ;
     // shouldComponentUpdate accepts a boolean, so the ternary operator will return true if the nextProps.value is even, and thus the component will update.
  }
  componentWillReceiveProps(nextProps) {
    console.log('Receiving new props...');
  }
  componentDidUpdate() {
    console.log('Component re-rendered.');
  }
  render() {
    return <h1>{this.props.value}</h1>
  }
};

class Controller extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      value: 0
    };
    this.addValue = this.addValue.bind(this);
  }
  addValue() {
    this.setState({
      value: this.state.value + 1
    });
  }
  render() {
    return (
      <div>
        <button onClick={this.addValue}>Add</button>
        <OnlyEvens value={this.state.value}/>
      </div>
    );
  }
};
```
### Introducing Inline Styles
If using a stylesheet, the className attributes of JSX elements can be used to apply styles w/ CSS.  
One can also use inline styles, e.g. 
In HTML, the inline styling might look like:
```HTML
<div style="color: Red; font-size: 100px">Big Red</div>
```
Whereas in JSX, it looks like:
```HTML
<div style={{color: "red", fontSize: 100}}>Big Red</div>
```
With the differences being the curly braces, quotation marks, comma v. semicolon use, camelCasing v. hyphenated, and lack of "px" designation for the fontSize.  The "px" is not needed b/c all sizes are assumed to be in pixels unless specified otherwise in JSX.  All property values except length-values using default pixels for a metric need to be wrapped in quotes.

### Add Inline Styles in React
In this example, the inline styling is added to the JSX as a variable using React.

```javascript
const styles = {color: "purple", fontSize: 40, border: "2px solid purple"}; //variable for elements of the styling

class Colorful extends React.Component {
  render() {
    return (
      <div style={styles}>Style Me!</div>
            //the styles variable is added inline.
    );
  }
};
```
### Use Advanced JavaScript in React Render Method
Instead of placing JavaScript inside curly braces in the JSX, it is possible to write JavaScript directly in the render method (before the return statement), then returning a variable name in curly braces into your JSX to call the JavaScript written in the render method.

This is used in the example, below, which returns an answer from a Magic Eight Ball :)
```javascript
const inputStyle = {
  width: 235,
  margin: 5
}

class MagicEightBall extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      userInput: '',
      randomIndex: ''
    }
    this.ask = this.ask.bind(this);
    this.handleChange = this.handleChange.bind(this);
  }
  ask() {
    if (this.state.userInput) {
      this.setState({
        randomIndex: Math.floor(Math.random() * 20),
        userInput: ''
      });
    }
  }
  handleChange(event) {
    this.setState({
      userInput: event.target.value
    });
  }
  render() {
    const possibleAnswers = [
      'It is certain',
      'It is decidedly so',
      'Without a doubt', 
      'Yes, definitely',
      'You may rely on it',
      'As I see it, yes',
      'Outlook good',
      'Yes',
      'Signs point to yes',
      'Reply hazy try again',
      'Ask again later',
      'Better not tell you now',
      'Cannot predict now',
      'Concentrate and ask again',
      'Don\'t count on it', 
      'My reply is no',
      'My sources say no',
      'Most likely',
      'Outlook not so good',
      'Very doubtful'
    ];
    const answer = possibleAnswers[this.state.randomIndex]
    //above return, javascript can be written directly
    return (
      <div>
        <input
          type="text"
          value={this.state.userInput}
          onChange={this.handleChange}
          style={inputStyle} /><br />
        <button onClick={this.ask}>
          Ask the Magic Eight Ball!
        </button><br />
        <h3>Answer:</h3>
        <p>
        {answer}
          { /* The variable is called in curly braces in JSX */ }
        </p>
      </div>
    );
  }
};
```
### Render with an If/Else Condition
In this example, there is an If/Else condition in the render method wherein the rendering is conditional.
```javascript
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      display: true
    }
    this.toggleDisplay = this.toggleDisplay.bind(this);
  }
  toggleDisplay() {
    this.setState({
      display: !this.state.display
    });
  }
  render() {
    if (this.state.display==true) {
    return (
       <div>
         <button onClick={this.toggleDisplay}>Toggle Display</button>
         <h1>Displayed!</h1>
       </div>
    );
    }
    else{
      return (
       <div>
         <button onClick={this.toggleDisplay}>Toggle Display</button>
       </div>
    );
    }
  }
};
```

### Use && for a More Concise Conditional
Instead of using If/Else syntax, as used above, one can use this syntax:
```javascript
{condition && <p>markup</p>}
 ```
 If the condition is true, the markup will be rendered.  If false, nothing w/in the curly braces will be rendered. 
 
 The following example has the exact same functionality as the example above, but is more concise.  Notice that this code:
 ```Javascript
{this.state.display &&<h1>Displayed!</h1>}
 ```
 takes the place of the if/else statement from the last example.
 ```javascript
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      display: true
    }
    this.toggleDisplay = this.toggleDisplay.bind(this);
  }
  toggleDisplay() {
    this.setState({
      display: !this.state.display
    });
  }
  render() {
   
    return (
       <div>
         <button onClick={this.toggleDisplay}>Toggle Display</button>
         {this.state.display &&<h1>Displayed!</h1>}
       </div>
    );
  }
};
```
### Use a Ternary Expression for Conditional Rendering
A ternary expression can be used for more complex conditionals, while still remaining more concise than if/else statements.
In the example below, the following ternary expression is used to load different buttons based on a person's age:
```javascript
{this.state.userAge === "" ? buttonOne : (this.state.userAge >=18) ? buttonTwo : buttonThree}
```
Notice that the ternary expression is placed in the JSX:

```javascript

const inputStyle = {
  width: 235,
  margin: 5
}

class CheckUserAge extends React.Component {
  constructor(props) {
    super(props);
    this.state = { 
      input: "",
      userAge: ""
    }
    this.submit = this.submit.bind(this);
    this.handleChange = this.handleChange.bind(this);
  }
  handleChange(e) {
    this.setState({
      input: e.target.value,
      userAge: ''
    });
  }
  submit() {
    this.setState({
      userAge: this.state.input
    });
  }
  render() {
    const buttonOne = <button onClick={this.submit}>Submit</button>;
    const buttonTwo = <button>You May Enter</button>;
    const buttonThree = <button>You Shall Not Pass</button>;
    return (
      <div>
        <h3>Enter Your Age to Continue</h3>
        <input
          style={inputStyle}
          type="number"
          value={this.state.input}
          onChange={this.handleChange} /><br />
        {this.state.userAge === "" ? buttonOne : (this.state.userAge >=18) ? buttonTwo : buttonThree}
      </div>
    );
  }
};
```
### Render Conditionally from Propss
In this example, the condition is based on props w/in a child component.
```javascript
class Results extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
      <h1>
  {
    this.props.fiftyFifty 
  }
  </h1>
    )
  };
};

class GameOfChance extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      counter: 1
    }
    this.handleClick = this.handleClick.bind(this);
  }
  handleClick() {
    this.setState({
      counter: this.state.counter + 1
    });
  }
  render() {
    let expression = Math.random() > .5
    return (
      <div>
        <button onClick={this.handleClick}>Play Again</button>
        {(expression==1) ? <Results fiftyFifty = "You win!" /> : <Results fiftyFifty = "You lose!" />}
        <p>{'Turn: ' + this.state.counter}</p>
      </div>
    );
  }
};
```
### Change Inline CSS Conditionally Based on Component State
Inline CSS can be changed based on conditional statements.  In the example, this if statement changes the styling variable, "inputStyle."
```javascript
if (this.state.input.length >15){
      inputStyle.border = "3px solid red";
```
The border is changed based on the number of characters in the input, which changes the state.

Here is the full example:
```javascript
class GateKeeper extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      input: ''
    };
    this.handleChange = this.handleChange.bind(this);
  }
  handleChange(event) {
    this.setState({ input: event.target.value })
  }
  render() {
    let inputStyle = {
      border: '1px solid black'
    };
    if (this.state.input.length >15){
      inputStyle.border = "3px solid red";
    }
    return (
      <div>
        <h3>Don't Type Too Much:</h3>
        <input
          type="text"
          style={inputStyle}
          value={this.state.input}
          onChange={this.handleChange} />
      </div>
    );
  }
};
```
### Use Array.map() to Dynamically Render Elements
This example creates a to-do list.  As the number of elements that neeed to be rendered is variable due to user input, map is used to render any amount of elements that are typed into the input.
Here is the map function: 
```javascript
const items = this.state.toDoList.map(a => <li>{a}</li>)
```
Notice that it is accepting a change to the state property, toDoList, and returning a li for each input.

Here is the full example:
```javascript
const textAreaStyles = {
  width: 235,
  margin: 5
};

class MyToDoList extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      userInput: "",
      toDoList: []
    }
    this.handleSubmit = this.handleSubmit.bind(this);
    this.handleChange = this.handleChange.bind(this);
  }
  handleSubmit() {
    const itemsArray = this.state.userInput.split(',');
    this.setState({
      toDoList: itemsArray
    });
  }
  handleChange(e) {
    this.setState({
      userInput: e.target.value
    });
  }
  render() {
    const items = this.state.toDoList.map(a => <li>{a}</li>);
    return (
      <div>
        <textarea
          onChange={this.handleChange}
          value={this.state.userInput}
          style={textAreaStyles}
          placeholder="Separate Items With Commas" /><br />
        <button onClick={this.handleSubmit}>Create List</button>
        <h1>My "To Do" List:</h1>
        <ul>
          {items}
        </ul>
      </div>
    );
  }
};
```
### Give Sibling Elements a Unique Key Attribute
The last example is missing its keys.  A key attribute allows changes to the state to be tracked, changed, or removed easily in re-rendering.  Sibling elements need unique keys.
Here is a list wherein the li elements are given unique keys:
```javascript
const frontEndFrameworks = [
  'React',
  'Angular',
  'Ember',
  'Knockout',
  'Backbone',
  'Vue'
];

function Frameworks() {
  const renderFrameworks = frontEndFrameworks.map(a => <li key={a+1}>{a}</li>)
                                                  //The keys are "elementName1"
  return (
    <div>
      <h1>Popular Front End JavaScript Frameworks</h1>
      <ul>
        {renderFrameworks}
      </ul>
    </div>
  );
};
```
### Use Array.filter() to Dynamically Filter an Array
This example uses filter to dynamically filter users into an array of users who are online.
While it could be filtered and mapped in the same line, this example splits it into two steps:
```javascript
const usersOnline = this.state.users.filter(a => a.online == true)
const renderOnline = usersOnline.map(b => <li key={b.username+1}>{b.username}</li>);
```
Here is the full example:
```javascript
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      users: [
        {
          username: 'Jeff',
          online: true
        },
        {
          username: 'Alan',
          online: false
        },
        {
          username: 'Mary',
          online: true
        },
        {
          username: 'Jim',
          online: false
        },
        {
          username: 'Sara',
          online: true
        },
        {
          username: 'Laura',
          online: true
        }
      ]
    }
  }
  render() {
    const usersOnline = this.state.users.filter(a => a.online == true)
    const renderOnline = usersOnline.map(b => <li key={b.username+1}>{b.username}</li>);
    return (
       <div>
         <h1>Current Online Users:</h1>
         <ul>
           {renderOnline}
         </ul>
       </div>
    );
  }
};
```
### Render React on the Server with renderToString
It is sometimes beneficial to render to the server (as opposed to the client, as has happened in every previous example).  Rendering the initial HTML markup to the server, for instance, would make it easier for search engines to crawl while simultaneously making the page load faster.

In this example, the component, "App," is rendered to the server using:
```javascript
ReactDOMServer.renderToString(<App />);
```
Here is the full example:
```javascript
class App extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return <div />
  }
};

ReactDOMServer.renderToString(<App />);
```