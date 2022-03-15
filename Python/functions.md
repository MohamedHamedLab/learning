# Functions

### Define a basic function

```python
def func1():
    print("i am a function")
```
### Function that takes arguments

```python
def func2(arg1, arg2):
    print(arg1, "", arg2)
```
### Function that returns a value

```python
def cube(x):
    return x*x*x
```
### Function with default value for an argument

```python
def power(num, x=1):
    result = 1
    for i in range(x):
        result = result * num
    return result
```
### Function with variable number of arguments

```python
def multi_add(*args):
    result = 0
    for x in args:
        result = result + x
    return result


func1()
print(func1())
print(func1)

func2(10, 20)
print(func2(10, 20))
print(cube(3))

print(power(2))
print(power(3, 5))
print(power(x=3, num=5))
print("test multi_add " + str(multi_add(2, 3, 4, 5, 6)))
```