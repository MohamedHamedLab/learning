# Essential Dart

## Built-In Types
- Dart has built-in types of numbers, strings, booleans, lists, maps, runes, and symbols.

## Using Enumerated Types
- type-safe way to declare a set of constant values.
 
```dart
enum TrafficColor { red, green, yellow }
var color = TrafficColor.red;
  switch (color) {
    case TrafficColor.red:
      print('stop');
      break;
    case TrafficColor.green:
      print('go');
      break;
    case TrafficColor.yellow:
      print('be careful');
  }
```
## Using Dynamic Type
- You don’t know the type of an object or you don’t care about the type.
```dart
dynamic value = 1;
print(value.runtimeType);
value = 'test';
if (value is String) {
  print('string');
}
```

## Understanding Functions
You want to understand functions in Dart.

```dart
int sum(List<int> list, [int initial = 0]) { // initial is optional parameter 
  var total = initial;
  list.forEach((v) => total += v);
  return total;
}
// Test
 assert(sum([1, 2, 3]) == 6);
```

## Using Typedefs
- You want to have an alias of a function type.

```dart
typedef Processor<T> = void Function(T value);

void process<T>(List<T> list, Processor<T> processor) {
  list.forEach((item) {
    print('processing $item');
    processor(item);
    print('processed $item');
  });
} 
// Test
process([1, 2, 3], print);
```

## Using Cascade Operator
- You want to make a sequence of operations on the same object.
```dart
class User {
  String name, email;
  Address address;
  void sayHi() => print('hi, $name');
}
class Address {
  String street, suburb, zipCode;
  void log() => print('Address: $street');
}
void main() {
  User()
    ..name = 'Alex'
    ..email = 'alex@example.org'
    ..address = (Address()
      ..street = 'my street'
      ..suburb = 'my suburb'
      ..zipCode = '1000'
      ..log())
    ..sayHi();
}
```

## Overriding Operators
- You want to override operators in Dart.
```dart
class Rectangle {
  int width, height;
  Rectangle(this.width, this.height);
  get area => width * height;
  bool operator <(Rectangle rect) => area < rect.area;
  bool operator >(Rectangle rect) => area > rect.area;
}
void main() {
  var rect1 = Rectangle(100, 100);
  var rect2 = Rectangle(200, 150);
  assert(rect1 < rect2);
  assert(rect2 > rect1);
}

```

## Using Constructors
- You want to create new instances of Dart classes.
```dart
class Rectangle {
  final num top, left, width, height;
  Rectangle(this.top, this.left, this.width, this.height); 
  Rectangle.fromPosition(this.top, this.left, num bottom, num right)
      : assert(right > left),
        assert(bottom > top),
        width = right - left,
        height = bottom - top;
  @override
  String toString() {
    return 'Rectangle{top: $top, left: $left, width: $width, height: $height}';
  }
}
void main(List<String> args) {
  var rect1 = Rectangle(100, 100, 300, 200);
  var rect2 = Rectangle.fromPosition(100, 100, 300, 200);
  print(rect1);
  print(rect2);
}

```
## Extending a Class
- You want to inherit behavior from an existing class.
- Extend from the existing class to create a subclass.


```dart
import 'dart:math' show pi;
abstract class Shape {
  double area();
}
class Rectangle extends Shape {
  double width, height;
  Rectangle(this.width, this.height);
  @override
  double area() {
    return width * height;
  }
}
class Square extends Rectangle {
  Square(double width) : super(width, width);
}
class Circle extends Shape {
  double radius;
  Circle(this.radius);
  @override
  double area() {
    return pi * radius * radius;
  }
}
void main() {
  var rect = Rectangle(100, 50);
  var square = Square(50);
  var circle = Circle(50);
  print(rect.area());
  print(square.area());
  print(circle.area());
}
 
```

## Adding Features to a Class
- You want to reuse a class’s code but are limited by single inheritance of Dart.
- how to use Use mixins.
- If you want to reuse code from multiple classes, mixins should be used.
- 
```dart
class Person {
  String name;
  Person(this.name);
}
class Student extends Person with CardHolder {
  Student(String name) : super('Student: $name') {
    holder = this;
  }
}
class Teacher extends Person with CardHolder {
  Teacher(String name) : super('Teacher: $name') {
    holder = this;
  }
}
mixin CardHolder {
  Person holder;
  void swipeCard() {
    print('${holder.name} swiped the card');
  }
}
mixin SystemUser {
  Person user;
  void useSystem() {
    print('${user.name} used the system.');
  }
}
class Assistant extends Student with SystemUser {
  Assistant(String name) : super(name) {
    user = this;
  }
}
```

## Using Interfaces
- You want to have a contract for classes to follow.

```dart
class DataLoader {
  void load() {
    print('load data');
  }
}
class CachedDataLoader implements DataLoader {
  @override
  void load() {
    print('load from cache');
  }
}
void main() {
  var loader = CachedDataLoader();
  loader.load();
}
```

### Using Generics
- You want to have type safety when your code is designed to work with different types.
- . With generics, we can add type parameters to classes and methods. Generics are usually used in collections to create type-safe collections. Listing
- shows the usage of generic collections in Dart. Dart generic types are reified, which means type information are available at runtime.
```dart
lass Calculator {
  T add<T extends num>(T v1, T v2) => v1 + v2;
  T subtract<T extends num>(T v1, T v2) => v1 - v2;
}
void main() {
  var calculator = Calculator();
  int r1 = calculator.add(1, 2);
  double r2 = calculator.subtract(0.1, 0.2);
  print(r1);
  print(r2);
}
```

## Using Libraries
```dart
import 'package:meta/meta.dart';
import 'lib1.dart' as lib1; //To avoid conflicts
import 'dart:math' show Random; // Use show to explicitly include members. Use hide to explicitly exclude members.
import 'dart:html' hide Element;
```

## Using Exceptions
- You want to deal with failures in Dart apps.

```dart
void main() {
  try {
    print(getNumber());
  } on ValueTooLargeException catch (e) {
    print(e);
    rethrow;
  } finally {
    print('in finally');
  }
}
```