# Loops
```python
x = 0
```
### Define a while loop
```python  
while (x < 5):
    print(x)
    x = x+1
```

### Define a for loop
```python  
for x in range(5, 10):
print(x)
```
### Use a for loop over a collection
 ```python  
days = ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"]
  for d in days:
      print(d)
 ```

using the enumerate() function to get index
The enumerate function will iterate over this collection like loop normally would,
but in addition to returning the value of the item being looked at,
it also returns a value that is the index of the item in question.
This function is going to return two values.
It's going to return the index of the member of the collection that we're looking at,
well as the actual member of the collection.
```python  
for i, d in enumerate(days):
    print(i, d)
```

### Use the break and continue statements
```python  
for x in range(5, 20):
    if(x == 17):
      break
    if(x % 2 == 0):
      continue
    print(x)
```