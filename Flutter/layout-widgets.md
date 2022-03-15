# Layout Widgets
- Layout in Flutter is implemented by a set of widgets. These layout widgets wrap other widgets to apply different layout constraints.

## Center Component
```dart
Center(
  widthFactor: 2.0,
  heightFactor: 2.0,
  child: Text("Center"),
)
```
## Aligning Widgets
```dart
Align(
  alignment: Alignment.topLeft,
  child: SizedBox(
    width: 200,
    height: 200,
    child: Center(
      child: Text("TopLeft"),
    ),
  ),
)
```

## Limiting Size to Allow Child Widget to Overflow
 -  widget to have a size and allow child widget to overflow use `SizedOverflowBox`
```dart
ConstrainedBox(
  constraints: BoxConstraints.loose(Size(100, 100)),
  child: SizedOverflowBox(
    size: Size(50, 50),
    child: Image.network('https://picsum.photos/400'),
  ),
)
```

## Adding Padding when Displaying Widgets

```dart
Padding(
  padding: EdgeInsets.all(20),
  child: Image.network('https://picsum.photos/200'),
)
```


## Transforming Widgets

```dart
Transform.rotate(
angle: pi / 4.0,
  origin: Offset(10, 10),
  child: Text('Hello World'),
)

 Transform.translate(
  offset: Offset(50, 50),
  child: Text('Hello World'),
)
```

## Implementing Flex Box Layout
- `Flexible` has the flex parameter to specify the flex factor and fit parameter to specify the BoxFit value.
-  `LimitedBox` widget to limit its height. All children of Column widget are non-flexible.

```dart
 LimitedBox(
  maxHeight: 320,
  child: Column(
    crossAxisAlignment: CrossAxisAlignment.end,
    mainAxisAlignment: MainAxisAlignment.spaceAround,
    children: <Widget>[
      Image.network('https://picsum.photos/50'),
      Image.network('https://picsum.photos/70'),
      Image.network('https://picsum.photos/90'),
    ],
  ),
)
LimitedBox(
  maxHeight: 300,
  child: Column(
    mainAxisAlignment: MainAxisAlignment.spaceBetween,
    children: <Widget>[
      Flexible(
        child: Image.network('https://picsum.photos/50'),
      ),
      Image.network('https://picsum.photos/40'),
      Expanded(
        child: Image.network('https://picsum.photos/50'),
      ),
      Expanded(
        flex: 2,
        child: Image.network('https://picsum.photos/50'),
      ),
    ],
  ),
)
```
