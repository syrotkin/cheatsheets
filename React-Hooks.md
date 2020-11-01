# React Hooks

## useState:
Adding state to a functional component
```javascript
const [value, setValue] = useState(initialState);
```

### Controlled input
```javascript
// initial name is ''
const [name, setName] = useState('');

// value of input is set to name (empty string initially)
// onChange, name is updated. So, the inputvalue is updated as well
<input type="text" onChange={(e) => setName(e.target.value)} value={name} />
```

## useEffect
somewhat analogous to lifecycle methods in class components

Runs after DOM has been updated, after every completed render.

```javascript
useEffect(() => {
    document.title = 'foo';
});
```


## useRef
Interacting with DOM nodes

```javascript
const ref = useRef();
```
On first render, `ref` is undefined. On second render, `ref.current` points to the DOM node.


### Usage:
```html
<div ref={ref}></div>
```

```javascript
console.log(ref.current.className);
```

## Context
Sharing state across the application

`createContext` is the hook

e.g.
```javascript
export const UserContext = createContext();
```

Wrapping DOM in context provider:
```html
<UserContext.Provider
    value={{
        user: true
    }}
>
    <div></div>
</UserContext.Provider>
```

### Usage:
```javascript
   import { UserContext } ...

   const userInfo = useContext(UserContext);
```

## useReducer
Similar to a redux reducer, but only available within component, **NOT** in global state.

Use case: state is complex. Otherwise: use `useState`.

```javascript
const reducer = (state, action) => {
    switch (action.type) {
        case 'add':
            return { count: state.count + 1 };
        // ...
    }
};

const initialState = { count: 0 };

const [state, dispatch] = useReducer(reducer, initialState);

// Call action of type 'add':
dispatch({ type: 'add' });
```

## useMemo

```javascript
const HeaderReversed = useMemo(() => reverseWord(title), [title]);
```