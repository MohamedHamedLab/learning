# Sorting

common sorting types are bubble sort, which is a very basic algorithm, that's mainly used as teaching tool these days, because it's really not very good. 

There's also the merge sort, which uses recursion to implement its main logic, 

and the quick sort, which also uses recursion and is usually even better than the merge sort.

 Each of these sorting algorithms illustrates a different way of tackling the problem of sorting information

## Bubble sort

So suppose we had an array of numbers like this. The bubble sort begins by comparing the first two elements to each other to see which is larger. If the first element is larger than the second, then the two elements are swapped. Then the algorithm advances to the next slot and performs the same comparison and again, swaps the values if the first one is larger.

So this process continues until we've examined all the items in the array and the largest value has made its way to the top. And that's why it's called the bubble sort. The values bubble their way to the top of the array. So after the largest value is in place, the process then starts all over again, but now, we only examine the elements up to the one before the last item and then the one before that and so on, until the array is fully sorted.

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f5343d8b-bb43-4a46-8bd5-082affa36f36/Screen_Shot_2020-02-05_at_8.32.36_AM.png](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/f5343d8b-bb43-4a46-8bd5-082affa36f36/Screen_Shot_2020-02-05_at_8.32.36_AM.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220312%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220312T000553Z&X-Amz-Expires=86400&X-Amz-Signature=417ff4a350c3c6b60d716be5d47c755304a88998ade4163495558ed08075872f&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Screen_Shot_2020-02-05_at_8.32.36_AM.png%22&x-id=GetObject)

```jsx
var a = [33, 103, 3, 726, 200, 984, 198, 764, 9];

function bubbleSort(a) {
    var swapped;
    do {
        swapped = false;
        for (var i=0; i < a.length-1; i++) {
            if (a[i] > a[i+1]) {
                var temp = a[i];
                a[i] = a[i+1];
                a[i+1] = temp;
                swapped = true;
            }
        }
    } while (swapped);
}

bubbleSort(a);
console.log(a);
```

### Merge Sort

The merge sort is known as a divide-and-conquer algorithm. It takes a given set of data and then breaks it down into smaller parts that are easier to work with. It uses recursion to break the data down and then sort the smaller sets of data, gradually working it's way back up to the original dataset. The merge sort has a very good performance profile. It typically operates on it's dataset in logarithmic time, giving it a big O of n log n.

Break Down

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b5640942-efb5-443f-a469-a1d06cab7fc4/Screen_Shot_2020-02-07_at_2.16.22_PM.png](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/b5640942-efb5-443f-a469-a1d06cab7fc4/Screen_Shot_2020-02-07_at_2.16.22_PM.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220312%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220312T000605Z&X-Amz-Expires=86400&X-Amz-Signature=3e1577431cf05626cde69dda6dffa4f8ff7f3c5d7cbe9c1ac70248330f856475&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Screen_Shot_2020-02-07_at_2.16.22_PM.png%22&x-id=GetObject)

Merge

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/21a46c9d-b3a3-4d59-8818-0a7b0e658c34/Screen_Shot_2020-02-07_at_2.15.56_PM.png](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/21a46c9d-b3a3-4d59-8818-0a7b0e658c34/Screen_Shot_2020-02-07_at_2.15.56_PM.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220312%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220312T000705Z&X-Amz-Expires=86400&X-Amz-Signature=74bd3d9f465b32ef5906bf4c6a25be625ddb99596fa3077717b8c589b5f9285f&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Screen_Shot_2020-02-07_at_2.15.56_PM.png%22&x-id=GetObject)

### Quick sort

its like the Merge Sort 

- it is also a divide and conquer algorithm and also uses recursion to perform its work, but usually performs better than the Merge Sort does.
- The Quick sort also performs the sorting of data in place in the existing array and doesn't need extra memory to do its work.
- The trade off is that the worst case scenario is when the list is already sorted or mostly sorted, in which case the performance can degrade to quadratic time complexity, but that's not common.So
- one of the main features of the Quick sort is the selection of what's called the Pivot Point