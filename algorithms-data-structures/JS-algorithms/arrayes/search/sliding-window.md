- Write a function accepts an array of integers and number called n, the function should calculate the maximum sum of n consecutive elements in array.
- 
**Example**
```js
// sum of the largest  n numbers
maxSubArraySum([1,2,3,5,2,8,1,5],2)
maxSubArraySum([1,2,5,2,8,1,1,5],2)
maxSubArraySum([4,2,2,6,1,5],2)
maxSubArraySum([3,8,1,5],2)
maxSubArraySum([],2) // null
```

**Function**
```js
 function maxSubArraySum(arr, num) {
     let maxSum = 0
     let tempSum = 0
     if (arr.length < num) return null;
     // sum first num numbers
     for (let i = 0; i < num; i++) {
         maxSum += arr[i]
     }
     tempSum = maxSum
     for (let i = num; i < arr.length; i++) {
         // fist number - next number then find the max number of both
         tempSum = tempSum - arr[i - num] + arr[i];
         maxSum = Math.max(maxSum, tempSum);
     }
     return maxSum
 }

 test('sliding window', () => {
     expect(maxSubArraySum([1, 2, 3, 5, 2, 8, 1, 5], 2)).toEqual(10)
     expect(maxSubArraySum([1, 2, 5, 2, 8, 1, 1, 5], 4)).toEqual(17)
     expect(maxSubArraySum([4, 2, 2, 6, 1, 5], 1)).toEqual(6)
     expect(maxSubArraySum([3, 8, 1, 5], 4)).toEqual(17)
     expect(maxSubArraySum([], 2)).toBeNull()
 });
```