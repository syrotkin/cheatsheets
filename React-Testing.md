# React Testing

## Mocking

Defining a mock function
```
const add = jest.fn((x, y) => 42);
```

Mocking the imported object
```
jest.mock('./add', () => {
	add: jest.fn(() => 42)
});
```

// override the mock implementation midway through the test
add.mockImplementation(() => 43);

## Test if null:
https://stackoverflow.com/questions/47259061/jest-enzyme-test-a-react-component-that-returns-null-in-render-method

ShallowWrapper::setState() can only be called on class components

```javascript
const component = mount(shallow(
      <PremiumDetail
        insuranceComparison={insuranceComparison}
        insuranceInquiryId="1"
        productBundleIds={[15, 19]}
        t={tMock}
        fetchingInsuranceComparison={false}
        fetchingInsuranceComparisonFailed={false}
        directDeal={1}
        currentBreakpoint=""
      />
    ).get(0));
```
	
Jest has a capability to use mocha syntax: describe, it
but also 'test' 

"react es 7 snippets" - VS Code plugin 

`rcc snippet` -> creates a simple React class component

## react-testing-library:
```
const wrapper = render(<Counter />); // creates wrapper (similar to enzyme)
wrapper.getByText();
wrapper.getByText('0') // is a DOM node
```
react-testing-library does the things the JavaScript way -- gets DOM nodes back, not shallow wrappers

```
wrapper.debug(); // prints out the DOM -- without needing to do console.log
```

## Test IDs - concept in react-teting-library
contrast with Enzyme - Enzyme uses component names
- but people don't work with components (claim of the series instructor) - they works with DOM elements.
react-testing-library way: Attach a data ID to DOM node

Actually uses `data-testid` in the elements - This way, we are using test code in your components. Some people frown upon it.

Example:
```html
<button data-testid="counter-button" />
```

Usage:
```
wrapper.getByTestId("counter-button")
```

Aside:
in `.eslintrc.js` we can define
```
"globals": {
	"test": true,
	"expect": true
}
```
Then VS code stops complaining about them not being imported

## Events in React Testing Library
Import `fireEvent` from `react-testing-library`
```
fireEvent.click(counterButton);
```
// cleanup is imported from `react-testing-library`

```
afterEach(cleanup);
```

## Enzyme vs. react-testing-library
`Enzyme`: key way to render: shallow rendering (`shallow`). But other ways exist: `mount`, `render`.

`react-testing-library`: default way: normal rendering. By default: full rendering, no shallow rendering
	
No shallow rendering in `react-testing-library`.

// the guy is a fan of using "data-testid"

`react-testing-library`:
```javascript
const { getByTestId, debug, queryByTestId } = render(<NewMovie />);
```

`react-testing-library` - integration testing by default


## Snapshot Testing:

```
expect(blah).toMatchSnapshot
```
e.g.
```javascript
test('<NewMovie />', () => {
  const {  container } = render(<NewMovie />);
  expect(container.firstChild).toMatchSnapshot();
});
```

The snapshot is generated under `__snapshots__/NewMovie.test.js.snap`. 

jest: Press 'u' in the console to regenerate snapshot (when the test breaks).

Case for snapshots: typos that lead to a snapshot test breaking, but the logic is intact, so that the other tests still pass.


## Spying mock functions

```javascript
const onSubmit = jest.fn();

const { getByText } = render(<MovieForm submitForm={onSubmit} />)

fireEvent.click(getByText('Submit'));

expect(onSubmit).toHaveBeenCalledTimes(1);
```

```javascript
  // Note: old syntax
  const label = getByLabelText('Text');
  label.value = 'hi';
  fireEvent.change(label);

  // Note: new syntax:
  fireEvent.change(getByLabelText('Text'), { 
    target: { value: 'hi' }
  });
```

#### Global mocks
You can mock external stuff, e.g.
```javascript
console.error = jest.fn();
```

#### Negative assertions
```javascript
expect(console.error).not.toHaveBeenCalled();
```

#### MemoryRouter
You can use `MemoryRouter` from `react-router-dom` to mock the router:
```javascript
import { MemoryRouter } from 'react-router-dom';

<MemoryRouter>
  <Movie />
</MemoryRouter>
```

#### mockClear
You need to clear the mocks in between the calls. Otherwise, the mock invocations may be recorded wrong.
e.g.  `console.error = jest.fn()` may be recorded as "invoked", once it has been invoked, even if it is not invoked in a particular test. To clear the mocks:

```javascript
afterEach(() => {
  cleanup();
  console.error.mockClear();
});
```

#### Mocking globals
Need package `jest-fetch-mock`.
`yarn add jest-fetch-mock`
or
`npm install jest-fetch-mock`

```javascript
  global.fetch = require('jest-fetch-mock');

  fetch.mockResponseOnce(JSON.stringify({
    movie: {
      id: "hi",
      title: "level up"
    }
  }));
```

#### waitForElement
To render an element that may be dependent on an AJAX call, use `waitForElement` (`react-testing-library`).
```javascript
await waitForElement(() => getByText('level up'));
// OR
await waitForElement(() => getByTestId('movie-title'));
```

Enzyme: tell to rerender (instead of waiting).

#### Code coverage
```
npm test --coverage
// or
yarn test --coverage
```

#### Resources on Testing
https://github.com/testing-library/react-testing-library

https://medium.com/@kentcdodds

(e.g. Why I never use shallow rendering)