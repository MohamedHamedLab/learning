# Algorithm

if you know algorithms you can use one of them in application you save time "Minimax Algorithms"

## Algorithms characteristics

### S**pace complexity:** which describes how much memory and storage space the algorithm needs to do its work

### Time complexity: which describes how efficient the algorithm is relative to the size of the input it is given to work on.

any given algorithm has a set of input values it can work on in order to produce a result. Sorting algorithms, for example, take a set of data values and attempt to put them into a specific order. It's also possible to talk about algorithm classification using a variety of criteria, just a few of which I've listed here.

## Common Algorithms

- **Searching Algorithm** : to find specific data in a structure (for example substring within a string)
- **Sorting algorithms**: take a dataset and apply a sort order to it.
- **Computational algorithms:** are used to take one set of data and derive another set of data from it. And a simple example might be calculating whether a given number is a prime number or maybe computing a temperature in one scale when you already have it in another scale.
- **Collection algorithms**: which involve manipulating or navigating among sets of data that are stored within a particular structure (example counting specific items, filtering out unwanted data)

## Measuring algorithm performance

**Big-O notation** used to describe algorithm performance, This notation format is used to describe how a particular algorithm performs as the size of the set of input grows over time.

And the reason the letter **O** is used is because the growth rate of an algorithm's time complexity is also referred to as the **order** of operation.

It usually describes the worst case scenario of how long it takes to perform a given operation. And it's important to note that many different algorithms and data structures have more than one Big-O value.

Data structures, for example, can usually perform multiple types of operations such as inserting or searching for values each of which have their own order of operation.

<aside>
💡 Example guessing Game : if you try to guess the right number between 1 to 15 by checking one by one that is called linear search because you where lined up in a row, or if you checked from the middle  then you go up or down  this approach called binary search

</aside>

## The common Big-O notation terms

0(1) - **Constant time:(**Looking up a single element in an array**)** that corresponds to a Big-O of one. And essentially that means that the operation in question doesn't depend on the number of elements in the given data set. So a good example of this is calculating whether a number is even or odd, or looking up a specific element index in an array.

**Log n - Logarithmic: (**Finding an item in a sorted Array with binary search**)** so as the number of items in the sorted array grows, it only takes a logarithmic time relationship to find any given item.

**Big-O of n - Linear time**,(Searching an unsorted array for specific value) and this level of time complexity corresponds to a typical example of searching for an item in an unsorted array. So as more items are added to the array in an unsorted fashion, it takes a corresponding linear amount of time to perform a search.

**n times log n- Log-linear** (Complex sorting algorithms like heap sort and merge sort) or what's called log-linear time complexity.

0(n2) **n squared - Quadratic**  (simple sorting algorithms, such as bubble sort selection sort, and inserting sort): which is called quadratic time complexity, and as you've probably guessed it's not a very good level of performance, because what that means is that as the number of items in the data set increases, the time it takes to process them increases at the square of that number.
 
![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/474beb50-6be1-4924-a3cc-62e1256ecf00/Screen_Shot_2019-12-02_at_8.49.36_AM.png](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/474beb50-6be1-4924-a3cc-62e1256ecf00/Screen_Shot_2019-12-02_at_8.49.36_AM.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220312%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220312T000259Z&X-Amz-Expires=86400&X-Amz-Signature=3a1fad50ebb5d37b183bfd60bec63fdcf13f53e6f998381903586e5671f098d1&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Screen_Shot_2019-12-02_at_8.49.36_AM.png%22&x-id=GetObject)
