# Binary search

Binary search is an efficient algorithm for finding an item from a sorted list of items. It works by repeatedly dividing in half the portion of the list that could contain the item, until you've narrowed down the possible locations to just one.

Here's a step-by-step description of using binary search to play the guessing game:

1. Let min = 1*min*=1m, i, n, equals, 1 and max = n*max*=*n*m, a, x, equals, n.
2. Guess the average of max*max*m, a, x and min*min*m, i, n, rounded down so that it is an integer.
3. If you guessed the number, stop. 
4. You found it!If the guess was too low, set min*min*m, i, n to be one larger than the guess.
5. If the guess was too high, set max*max*m, a, x to be one smaller than the guess.
6. Go back to step two.

### Implementing binary search of an array

**pseudocode** for binary search, modified for searching in an array. The inputs are the array, which we call `array`; the number `n` of elements in `array`; and `target`, the number being searched for. The output is the index in `array` of `target`:

1. Let `min = 0` and `max = n-1`.
2. Compute `guess` as the average of `max` and `min`, rounded down (so that it is an integer).
3. If `array[guess]` equals `target`, then stop. You found it! Return `guess`.
4. If the guess was too low, that is, `array[guess] < target`, then set `min = guess + 1`.
5. Otherwise, the guess was too high. Set `max = guess - 1`.
6. Go back to step 2.

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/160f09e4-4a43-4e87-95b9-48ca1c2b3a31/guess_1.png](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/9b210fa8-fc93-4769-875c-d376b5fc93e5/guess_2.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220312%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220312T000001Z&X-Amz-Expires=86400&X-Amz-Signature=8d78f9a0e8d21d711a5111d8294f6c9bc81119e5fb973d1694edf6fbff012e68&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22guess_2.png%22&x-id=GetObject)

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9b210fa8-fc93-4769-875c-d376b5fc93e5/guess_2.png](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/9b210fa8-fc93-4769-875c-d376b5fc93e5/guess_2.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220312%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220312T000001Z&X-Amz-Expires=86400&X-Amz-Signature=8d78f9a0e8d21d711a5111d8294f6c9bc81119e5fb973d1694edf6fbff012e68&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22guess_2.png%22&x-id=GetObject)

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c4186b22-9c4f-4da7-94b5-839b51ecbf89/guess_3.png](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/c4186b22-9c4f-4da7-94b5-839b51ecbf89/guess_3.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220312%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220312T000226Z&X-Amz-Expires=86400&X-Amz-Signature=9c4d41502216dd96ea2dfba56b51921fc4428a5a930d0abca039ba585f4cffd6&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22guess_3.png%22&x-id=GetObject)

### Implementing pseudocode

How would we turn that pseudocode into a JavaScript program? We should create a function, because we're writing code that accepts an input and returns an output, and we want that code to be reusable for different inputs. The parameters to the function—let's call it binarySearch— will be the array and target value, and the return value of the function will be the index of the location where the target value was found.

Here is modified pseudocode for binary search that handles the case in which the target number is not present:

1. Let `min = 0` and `max = n-1`.
2. If `max < min`, then stop: `target` is not present in `array`.Return `-1`.
3. Compute `guess` as the average of `max` and `min`, rounded down (so that it is an integer).
4. If `array[guess]` equals `target`, then stop. You found it! Return `guess`.
5. If the guess was too low, that is, `array[guess] < target`, then set `min = guess + 1`.Otherwise, the guess was too high. 
6. Set `max = guess - 1`.Go back to step 2.