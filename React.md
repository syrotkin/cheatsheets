## Rendering
```javascript
ReactDOM.render(JSX, document.getElementById('root'));
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
    return (<div><h1>Some text</h1></div>);
  }
};
```