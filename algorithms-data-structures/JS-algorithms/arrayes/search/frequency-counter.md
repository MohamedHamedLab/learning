- Write a function accepts two arrays and return true if every value in the array has it;s corresponding value squared in the seconde array.

**Examples**

same([1,2,3], [4,1,9]) // true
same([2,1,2], [1,9]) // false
same([1,2,1], [4,4,1]) // false

**result**
```js
function same(arr1, arr2) {
    //return false, if they are not same length 
    if (arr1.length !== arr2.length) {
        return false
    }
    let freqCounter1 = {}
    let  freqCounter2 = {}
    for (let val of arr1) {
        freqCounter1[val] = (freqCounter1[val] || 0) + 1
    }
    for (let val of arr2) {
        freqCounter2[val] = (freqCounter2[val] || 0) + 1
    }
    for (let key in freqCounter1) {
        if (!(key ** 2 in freqCounter2)) {
            return false
        }
        if (freqCounter2[key ** 2] !== freqCounter1[key]) {
            return false
        }
    }
    return true
}

test('frequency counter', () => {
    expect(same([1, 2, 3], [4, 1, 9])).toBeTruthy()
    expect(same([1, 2, 3], [4, 1])).toBeFalsy()
    expect(same([1, 2, 3], [9,4, 1])).toBeTruthy()
    expect(same([1, 2, 4], [9,4, 1])).toBeFalsy()
});
```
