# Matchers 
**Common Matchers**

**ToBe**

- The simplest way to test a value is with exact equality.

```jsx
test('two plus two is four', () => {
expect(2 + 2).toBe(4);
});
```

**ToEqual**

- toEqual recursively checks every field of an object or array.

```jsx
test('object assignment', () =>
{
const data = {one: 1};

data['two'] = 2;

expect(data).toEqual({one: 1, two: 2});

});
```

**Truthiness**

```jsx
toBeNull, toBeUndefined, toBeDefined, toBeTruthy, toBeFalsy,
```

```jsx
test('null', () => {
  const n = null;
  expect(n).toBeNull();
  expect(n).toBeDefined();
  expect(n).not.toBeUndefined();
  expect(n).not.toBeTruthy();
  expect(n).toBeFalsy();
);
  
test('zero', () => {
  const z = 0;
    expect(z).not.toBeNull();
    expect(z).toBeDefined();
    expect(z).not.toBeUndefined();
    expect(z).not.toBeTruthy();
    expect(z).toBeFalsy();
  });
```

**Numbers**

Most ways of comparing numbers have matcher equivalents.

toBeGreaterThan, toBeGreaterThanOrEqual, toBeLessThan, toBeLessThanOrEqual

```jsx
test('two plus two', () => {
 const  value = 2 + 2;
expect(value).toBeGreaterThan(3);
expect(value).toBeGreaterThanOrEqual(3.5);
expect(value).toBeLessThan(5);
 // toBe and toEqual are equivalent for numbers
expect(value).toBeLessThanOrEqual(4.5);
expect(value).toBe(4); expect(value).toEqual(4);

});
```

**Strings**

toMatch

```jsx
test('there is no I in team', () => {
expect('team').not.toMatch(/I/);
});

test('but there is a "stop" in Christoph', () => {
expect('Christoph').toMatch(/stop/);
});
```

**Arrays and iterables**

toContain

```jsx
test('the shopping list has beer on it', () => {
expect(shoppingList).toContain('beer');
expect(new  Set(shoppingList)).toContain('beer');
});
```

**Exceptions, errors**

toThrow