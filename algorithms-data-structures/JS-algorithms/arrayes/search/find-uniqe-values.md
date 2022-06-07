- Write a function accepts a sorted array, and counts the unique values in the array.



```js
function countUniqueValues(arr) {
    if (arr.length === 0) return 0
    var i = 0
    for(var j= 1;j < arr.length ; j++){
        if(arr[i] !== arr[j]){
            i++;
            arr[i] = arr[j]
        }
    }
    return i + 1

}

test('count unique value', () => {
    // 
    expect(countUniqueValues([1,1,1,1,1,2,3])).toEqual(3)
    expect(countUniqueValues([1,2,4,4,4,4,4,7,7,12,12,13])).toEqual(6)
    expect(countUniqueValues([-2,-1,-1,0,1,1])).toEqual(4) 
});
```