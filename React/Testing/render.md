# Render

### Integration testing

```jsx
// Unit test
// It only tests one thing
test('add', () => {
  expect(add(1, 2)).toBe(3);
  expect(add(5, 2)).toBe(7);
});

// Integration tests
// Tests things working together
test('total', () => {
  expect(total(5, 20)).toBe('$25');
});
```

### Render Component

```jsx
import React from 'react';
import { render, cleanup, fireEvent } from 'react-testing-library';
import Counter from './Counter';

test('<Counter />', () => {
  // Renders component
  const wrapper = render(<Counter />);

  wrapper.debug(); // Outputs dom as string

  // Asserts text value 0 is found within a button
  expect(wrapper.getByText('0').tagName).toBe('BUTTON');
});
```

### trigger click

```jsx
import { render, cleanup, fireEvent } from 'react-testing-library';

afterEach(cleanup);

test('<Counter />', () => {
  // Renders component
  const { debug, getByTestId } = render(<Counter />);

  // debug(); // Outputs dom as string
  const counterButton = getByTestId('counter-button');

  // Asserts counter-button is a button
  expect(counterButton.tagName).toBe('BUTTON');
  // Asserts counter-button starts at 0
  expect(counterButton.textContent).toBe('0');

  fireEvent.click(counterButton);
  expect(counterButton.textContent).toBe('1');

  fireEvent.click(counterButton);
  expect(counterButton.textContent).toBe('2');
  // debug(); // Outputs dom as string
});
```

## getByTestId & queryByTestId
```jsx
test('<NewMovie>', () => {
  const { debug, getByTestId, queryByTestId } = render(<NewMovie />);
  expect(getByTestId('page-title').textContent).toBe('New Movie');
  expect(queryByTestId('movie-form')).toBeTruthy();

  debug();
});
```