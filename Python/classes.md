# Classes

```python
class myClass():
    def method1(self):
      print("myclass method1")
    def method2(self, someString):
      print("myclass method2 "+ someString)
      
class anotherClass(myClass):
    def method1(self):
      print("myclass method1")
    def method2(self, someString):
      print("myclass method2 ")
def main():
    c= myClass()
    c.method1()
    c.method2("this is a string")
    c1= anotherClass()
    c1.method1()
    c1.method2("this is a string 2")
```