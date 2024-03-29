## Environment variables
In code:
```javascript
const baseUrl = process.env.REACT_APP_BASE_URL;
```
Variables have to start with `REACT_APP_`

In `.env` file:
```
REACT_APP_BASE_URL=https://localhost:9090/
```

In `.gitignore`
```
.env
```

## Importing
```javascript
import React, { PropTypes } from 'react';
```

## Rendering
```javascript
ReactDOM.render(JSXElement, document.getElementById('root'));
ReactDOM.render(<ComponentToRender/>, document.getElementById('root'));
```

## Comments in JSX

```javascript
<div>
{ /* this is a comment */ }
</div>
```

## Components


```javascript
// Stateless functional component
const MyComponent1 = function() {
  return (<div>Some text</div>);
};
```

```javascript
class MyComponent2 extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
        <div>
        <h1>Some text</h1>
        <MyComponent1/> { /* Composition! */ }
        </div>);
  }
};
```

## Passing properties to child components
### Reading the custom `date` property in a *stateless functional* child component
```javascript
const CurrentDate = (props) => {
  return (
    <div>
      <p>The current date is: {props.date}</p>
    </div>
  );
};
```

### Reading the custom `date` property in an *ES6 class* child component: use `this`:
```javascript
class CurrentDate extends React.Component {
    constructor(props) {
        super(props);
    }

    render() {
        return (
            <div>
      <p>The current date is: {this.props.date}</p>
    </div>
        );
    }
}
```
### Passing the `date` property to the child component
```javascript
class Calendar extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
      <div>
        <CurrentDate date={Date()} />
      </div>
    );
  }
};
```

## Default properties
If `props` is not passed to a component, a value from `defaultProps` is used.

```javascript
MyComponent.defaultProps = {location: 'Berlin'};
```

## Typechecking with propTypes
https://reactjs.org/docs/typechecking-with-proptypes.html

```javascript
MyComponent.propTypes = {age: PropTypes.number.isRequired, name: PropTypes.string.isRequired };
```

## State

### Using state in a component
`state` has to be set in the constructor and it has to be an object.
```javascript
class MyComponent extends React.Component {
    constructor(props) {
        super(props);
        this.state = {name: 'Bob'};
    }
    render() {
        return (<h1>{this.state.name}</h1>);
    }
}
```

### Setting state

React expects you to never modify state directly, instead use `this.setState()` when state changes occur. This is to be used in the other class methods of the component (not the constructor).

```javascript
this.setState({name: 'Bob'});
```

## Binding `this`

`this` in the instance methods of the component needs to be the same as `this` in the constructor. Therefore, it needs to be bound as follows:

```javascript
constructor(props) {
  super(props);
  this.state = {
    input: ''
  };
  // binding, so that 'this' is available to handleChange
  this.handleChange = this.handleChange.bind(this);
}

// the instance method where 'this'is available now
handleChange(event) {
  this.setState({input: event.target.value}); 
}
```

## Event Listeners

```javascript
componentDidMount() {
  document.addEventListener('keydown', this.handleKeyPress);

}
componentWillUnmount() {
  document.removeEventListener('keydown', this.handleKeyPress);
}
```