# Common Data Structure

The data structures that you will probably most commonly work with are arrays, linked lists, stacks and queues, trees, and hash tables.

### Arrays

Array is a container which can hold a fix number of items and these items should be of the same type. Most of the data structures make use of arrays to implement their algorithms.

The concept of Array:

- **Element** − Each item stored in an array is called an element.
- **Index** − Each location of an element in an array has a numerical index, which is used to identify the element.
    
    ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3a0a3209-21ab-4f3e-bdda-b21b46839221/array.jpg](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/3a0a3209-21ab-4f3e-bdda-b21b46839221/array.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220312%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220312T230618Z&X-Amz-Expires=86400&X-Amz-Signature=a7b8d9fd2ccd2a3cbe25a7c7f88d5b325f139656732aec827c4c795ab48038da&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22array.jpg%22&x-id=GetObject)
    

Basic Operations supported by array :

- **Traverse** − print all the array elements one by one.
- **Insertion** − Adds an element at the given index.
- **Deletion** − Deletes an element at the given index.
- **Search** − Searches an element using the given index or by the value.
- **Update** − Updates an element at the given index.

### Linked lists

Linked List is a sequence of links which contains items. Each link contains a connection to another link. Linked list is the second most-used data structure after array.

The concept of Linked List:

- **Link** − Each link of a linked list can store a data called an element.
- **Next** − Each link of a linked list contains a link to the next link called Next.
- **LinkedList** − A Linked List contains the connection link to the first link called First.

### Stacks and Queues

A stack is a collection of elements that supports two principle operations, push and pop.

Stacks are last-in, first-out data structures. In other words, the last item pushed is the first one popped.

- Pushing an item onto the stack is a constant-time operation since it doesn't matter how many items are already on the stack.
- Then we could take that stack and pop an item off to operate on it. And again, that's a constant-time operation.
- Queues work a little bit differently. So like a stack, the queue structure supports adding and removing items, but it operates in a first-in, first-out method.
- So if we had an empty queue and added an item in, it would be the first item in the list.

### Hash tables - dictionaries.

A hash table is a form of what's called an associative array. It's a data structure that maps keys to their associated values, and it does this using what's called a hash function.

This function uses the key to compute an index into the slots that are in the hash table and map the key to the value.

One of the primary benefits of hash tables is their ability to uniquely map a given key to a specific value.

Another advantage of hash tables is their speed. They are typically faster than other kinds of table lookup structures, particularly when the number of entries is large.

have some drawbacks, however. If the number of entries in the hash table are small, then it might be more efficient to just use a regular array or a linked list.