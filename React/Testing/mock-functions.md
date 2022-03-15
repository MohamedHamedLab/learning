# Mock Functions
### Create mock

- Mock functions make it easy to test the links between code by erasing the actual 

implementation of a function.

```jsx
/ This is dumb in practice, but a needed
// technical skill.
// Do not create mock functions and test them
// in the real world
const add = jest.fn(() => 3);

// Unit test
// It only tests one thing
test('add', () => {
  expect(add(1, 2)).toBe(3);
  expect(add).toHaveBeenCalledTimes(1);
  expect(add).toHaveBeenCalledWith(1, 2);
  // expect(add(5, 2)).toBe(7);
});
```

### Mock Nest function with integration test

```jsx
import { add } from './add';

jest.mock('./add', () => ({
  add: jest.fn(() => 25)
}));

// Integration tests
// Tests things working together
test('total', () => {
  expect(total(5, 20)).toBe('$25');
  expect(add).toHaveBeenCalledTimes(1);

  // Redundant
  add.mockImplementation(() => 30);
  expect(total(5, 25)).toBe('$30');
  expect(add).toHaveBeenCalledTimes(2);
});
```

**.Mock property**

All mock functions have this special .mock property, which is where data about how the function has been called and what the function returned is kept. The .mock property also tracks the value of this for each call, so it is possible to inspect this as well

```jsx
const myMock = jest.fn();
const a = new myMock();
const b = {};
const bound = myMock.bind(b);
bound();
console.log(myMock.mock.instances);
// > [ <a>, <b> ]

//these mock members are very useful in tests to assert how these functions 
//get called, instantiated, or what they returned:
// The function was called exactly once

expect(someMockFunction.mock.calls.length).toBe(1);

// The first arg of the first call to the function was 'first arg'
expect(someMockFunction.mock.calls[0][0]).toBe('first arg');

// The second arg of the first call to the function was 'second arg'
expect(someMockFunction.mock.calls[0][1]).toBe('second arg');

// The return value of the first call to the function was 'return value'
expect(someMockFunction.mock.results[0].value).toBe('return value');

// This function was instantiated exactly twice
expect(someMockFunction.mock.instances.length).toBe(2);
// The object returned by the first instantiation of this function

// had a `name` property whose value was set to 'test'
expect(someMockFunction.mock.instances[0].name).toEqual('test’);
```

**Mock Return Values**

```jsx
const myMock = jest.fn();
console.log(myMock());

// > undefined

myMock
.mockReturnValueOnce(10)
.mockReturnValueOnce('x')
.mockReturnValue(true);

console.log(myMock(), myMock(), myMock(), myMock());

// > 10, 'x', true, true
```

### Reset mock & add router

```jsx
import React from 'react';
import { render, cleanup } from 'react-testing-library';
import { MemoryRouter } from 'react-router-dom';
import Movie from './Movie';

afterEach(() => {
  cleanup();
// clear mock after each test
  console.error.mockClear();
});

console.error = jest.fn();

test('<Movie />', () => {
  render(<Movie />);
  expect(console.error).toHaveBeenCalled();
});

const movie = {
  id: 'hi',
  title: 'Level Up Big Day Out',
  poster_path: 'adsfadsfa.jpg',
};

test('<Movie /> with movie', () => {
  render(
    <MemoryRouter>
      <Movie movie={movie} />
    </MemoryRouter>,
  );
  expect(console.error).not.toHaveBeenCalled();
});
```