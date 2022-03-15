
#
#  Widget Basics

## BuildContext
- To access information related to a widget in the widgets tree
- BuildContext is actually the interface of Element class. In StatelessWidget.build() and State.build() methods , the BuildContext object represents the location where the current widget is inflated
```dart
class WithBuildContext extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    Column column = context.ancestorWidgetOfExactType(Column);
    return Text(column.children.length.toString());
  }
}
```

## Stateless Widget
- To create a widget that has no mutable state.
```dart
class HelloWorld extends StatelessWidget {
  const HelloWorld({Key key}) : super(key: key);
  @override
  Widget build(BuildContext context) {
    return Center(
      child: Text('Hello World!'),
    );
  }
}
```

## Stateful Widget
-  To create a widget that has mutable state.
  
```dart
class Counter extends StatefulWidget {
  @override
  _CounterState createState() => _CounterState();
}
class _CounterState extends State<Counter> {
  int value = 0;
  @override
  Widget build(BuildContext context) {
    return Row(
      children: <Widget>[
        Text('$value'),
        RaisedButton(
          child: Text('+'),
          onPressed: () {
            setState(() {
              value++;
            });
          },
        ),
      ],
    );
  }
}
```

## Inherited Widget
- propagate data down the widgets tree.

```dart
class ConfigWidget extends InheritedWidget {
  const ConfigWidget({
    Key key,
    @required this.config,
    @required Widget child,
  })  : assert(config != null),
        assert(child != null),
        super(key: key, child: child);
  final String config;
  static String of(BuildContext context) {
    final ConfigWidget configWidget =
        context.inheritFromWidgetOfExactType(ConfigWidget);
    return configWidget?.config ?? 
   }
  @override
  bool updateShouldNotify(ConfigWidget oldWidget) {
    return config != oldWidget.config;
  }
```

## Displaying Text
```dart
Text(
  'Bigger Bold Text',
  style: TextStyle(fontWeight: FontWeight.bold),
  textScaleFactor: 2.0,
);
Text(
  'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt',
  maxLines: 1,
  overflow: TextOverflow.ellipsis,
);

// to apply text style 
Text(
  'Decoration',
  style: TextStyle(
    fontWeight: FontWeight.w900,
    decoration: TextDecoration.lineThrough,
    decorationStyle: TextDecorationStyle.dashed,
  ),
);

```
### Args
- style:Style of the text.
- textAlign:  How text should be aligned horizontally.
- textDirection: direction of text.
- Locale: Locale to select font based on Unicode.
- softWrap: Whether to break text at soft line breaks.
- overflow: How to handle text overflow.
- textScaleFactor: The factor to scale the text.
- maxLines: The maximum number of lines. If the text exceeds the limit, it will be truncated according to the strategy specified in overflow.
- semanticsLabel: Semantics label for the text.

## TextSpan
 
```dart
Text.rich(TextSpan(
  style: TextStyle(
    fontSize: 16,
  ),
  children: [
    TextSpan(text: 'The quick brown '),
    TextSpan(
        text: 'fox',
        style: TextStyle(
          fontWeight: FontWeight.bold,
          color: Colors.red,
        )),
    TextSpan(text: ' jumps over the lazy '),
    TextSpan(
        text: 'dog',
        style: TextStyle(
          color: Colors.blue,
        )),
  ],
));

```

## RichText
```dart
RichText(
  text: TextSpan(
    text: 'Level 1',
    style: TextStyle(color: Colors.black),
    children: [
      TextSpan(
        text: 'Level 2',
        style: TextStyle(fontWeight: FontWeight.bold),
        children: [
          TextSpan(
            text: 'Level 3',
            style: TextStyle(color: Colors.red),
          ),
        ],
      ),
    ],
  ),
);
```

## Displaying Images
- All downloaded images are cached regardless of HTTP headers.
```dart
Image.network('https://picsum.photos/400/300',
  width: 400,
  height: 300,
);

// or
SizedBox(
  width: 400,
  height: 300,
  child: Image.network(
    'https://picsum.photos/300/200',
    alignment: Alignment.topLeft,
    repeat: ImageRepeat.repeat,
  ),
);
```

## Displaying Icons

```dart
// using matrial icons https://​material.​io/​tools/​icons/​
Icon(
  Icons.call,
  size: 100,
  color: Colors.red,
);

//or using external icons https://pub.dartlang.org/packages/font_awesome_flutter 
Icon(
  FontAwesomeIcons.angry,
  size: 80,
)
```

 
 ## Buttons
- Use button widgets TextButton, ElevatedButton, OutlinedButton.
```dart
// TextButton
TextButton(
  style: ButtonStyle(
    foregroundColor: MaterialStateProperty.all<Color>(Colors.blue),
    overlayColor: MaterialStateProperty.resolveWith<Color?>(
      (Set<MaterialState> states) {
        if (states.contains(MaterialState.hovered))
          return Colors.blue.withOpacity(0.04);
        if (states.contains(MaterialState.focused) ||
            states.contains(MaterialState.pressed))
          return Colors.blue.withOpacity(0.12);
        return null; // Defer to the widget's default.
      },
    ),
  ),
  onPressed: () { },
  child: Text('TextButton')
)
// ElevatedButton
final ButtonStyle raisedButtonStyle = ElevatedButton.styleFrom(
  onPrimary: Colors.black87,
  primary: Colors.grey[300],
  minimumSize: Size(88, 36),
  padding: EdgeInsets.symmetric(horizontal: 16),
  shape: const RoundedRectangleBorder(
    borderRadius: BorderRadius.all(Radius.circular(2)),
  ),
);

ElevatedButton(
  style: raisedButtonStyle,
  onPressed: () { },
  child: Text('Looks like a RaisedButton'),
)

// OutlinedButton
final ButtonStyle outlineButtonStyle = OutlinedButton.styleFrom(
  primary: Colors.black87,
  minimumSize: Size(88, 36),
  padding: EdgeInsets.symmetric(horizontal: 16),
  shape: const RoundedRectangleBorder(
    borderRadius: BorderRadius.all(Radius.circular(2)),
  ),
).copyWith(
  side: MaterialStateProperty.resolveWith<BorderSide>(
    (Set<MaterialState> states) {
      if (states.contains(MaterialState.pressed))
        return BorderSide(
          color: Theme.of(context).colorScheme.primary,
          width: 1,
        );
      return null; // Defer to the widget's default.
    },
  ),
);

OutlinedButton(
  style: outlineButtonStyle,
  onPressed: () { },
  child: Text('Looks like an OutlineButton'),
)


IconButton(
  icon: Icon(Icons.map),
  iconSize: 50,
  tooltip: 'Map',
  onPressed: () => {},
);
```

## Adding Placeholders
- add placeholders to represent widgets that will be added later.

```dart
Placeholder(
  color: Colors.red,
  strokeWidth: 1,
  fallbackHeight: 200,
  fallbackWidth: 200,
);

```

## Material Design Dialogs
- Use showDialog() function and Dialog, SimpleDialog, and AlertDialog widgets.

```dart
RaisedButton(
  child: Text('Show SimpleDialog'),
  onPressed: () async {
    String result = await showDialog<String>(
        context: context,
        builder: (BuildContext context) {
          return SimpleDialog(
            title: Text('Choose Color'),
            children: <Widget>[
              SimpleDialogOption(
                child: Text('Red'),
                onPressed: () {
                  Navigator.pop(context, 'Red');
                },
              ),
              SimpleDialogOption(
                child: Text('Green'),
                onPressed: () {
                  Navigator.pop(context, 'Green');
                },
              ),
            ],
          );
        });
    print(result);
  },
);
//shows an alert dialog with two actions.
RaisedButton(
  child: Text('Show AlertDialog'),
  onPressed: () async {
    bool result = await showDialog<bool>(
 context: context,
      builder: (BuildContext context) {
        return AlertDialog(
          title: Text('Delete'),
          content: Text('Delete this item?'),
          actions: <Widget>[
            FlatButton(
              child: Text('Yes'),
              onPressed: () {
                Navigator.pop(context, true);
              },
            ),
            FlatButton(
              child: Text('No'),
              onPressed: () {
                Navigator.pop(context, false);
              },
            ),
          ],
        );
      },
    );
    print(result);
  },
);     
```

