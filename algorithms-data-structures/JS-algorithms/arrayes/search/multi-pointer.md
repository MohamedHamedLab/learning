- Write a pointers or values that correspond to index or position and moved to the end or middle or beginning based on certan condation

**Example**
```js
sumZero([-4, -3, -2, -1, 0, 1, 2, 3]) //[-3, 3]
sumZero(sumZero([1,2,3]) // Undefined
```

```jsx
function sumZero(arr) {
    for (let i = 0; i < arr.length; i++) {
        for (let j = i + 1; j < arr.length; j++) {
            if (arr[i] + arr[j] === 0) {
                return [arr[i], arr[j]]
            }
        }
    }
} 
//or 
function sumZero(arr) {
    let left = 0
    let right = arr.length - 1;
    while (left < right) {
        let sum = arr[left] + arr[right];
        if (sum === 0) {
            return [arr[left], arr[right]]
        } else if (sum > 0) {
            right--
        } else {
            left++
        }
    }
}

test('multi pointer', () => {
    expect(sumZero([-4, -3, -2, -1, 0, 1, 2, 3])).toEqual([-3, 3])
    expect(sumZero([1,2,3])).toBeUndefined()
    expect(sumZero([-2, 1, 3])).toBeUndefined()
});
```