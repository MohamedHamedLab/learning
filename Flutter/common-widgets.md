# Common Widgets

## List of Items

```dart
ListView(
  children: <Widget>[
    ExampleWidget(name: 'Box 1'),
    ExampleWidget(name: 'Box 2'),
    ExampleWidget(name: 'Box 3'),
  ],
)
 //ListView with Item Builders
ListView.builder(
  itemCount: 20,
  itemBuilder: (context, index) {
    return ExampleWidget(name: 'Dynamic Box ${index + 1}');
  },
);

ListView.separated(
itemBuilder: (context, index) {
    return ExampleWidget(name: 'Separated Box ${index + 1}');
  },
  separatorBuilder: (context, index) {
    return Divider(
      height: 8,
    );
  },
  itemCount: 20,
);
// ListTile
ListTile(
  title: Text('Title'),
  subtitle: Text('Description'),
  leading: Icon(Icons.shop),
  trailing: Icon(Icons.arrow_right),
)
```

## Grid
- Use GridView.
```dart
 GridView.count(
  crossAxisCount: 3,
  children: List.generate(10, (index) {
    return ExampleWidget(
      name: 'Fixed Count ${index + 1}',
    );
  }),
);


// with header and footer 
GridView.count(
  crossAxisCount: 2,
  children: <Widget>[
    GridTile(
      child: ExampleWidget(name: 'Simple'),
    ),
    GridTile(
      child: ExampleWidget(name: 'Header & Footer'),
      header: GridTileBar(
        title: Text('Header'),
        backgroundColor: Colors.red,
      ),
      footer: GridTileBar(
        title: Text('Footer'),
        subtitle: Text('Description'),
        backgroundColor: Colors.blue,
      ),
    )
  ],
);
```

## table layout
- Use Table widget.

```dart
 Table(
  border: TableBorder.all(color: Colors.red.shade200),
  children: [
    TableRow(children: [Text('A'), Text('B'), Text('C'), Text('D')]),
    TableRow(children: [Text('E'), Text('F'), Text('G'), Text('H')]),
    TableRow(children: [Text('I'), Text('J'), Text('K'), Text('L')]),
  ],
);

//  table with different column width.
Table(
border: TableBorder.all(color: Colors.blue.shade200),
  columnWidths: {
    0: FixedColumnWidth(100),
    1: FlexColumnWidth(1),
    2: FlexColumnWidth(2),
    3: FractionColumnWidth(0.2),
  },
  children: [
    TableRow(children: [Text('A'), Text('B'), Text('C'), Text('D')]),
    TableRow(children: [Text('E'), Text('F'), Text('G'), Text('H')]),
    TableRow(children: [Text('I'), Text('J'), Text('K'), Text('L')]),
  ],
);


```

## Scaffolding Material Design Pages

### AppBar 
```dart
 AppBar(
  title: Text('Scaffold'),
  actions: <Widget>[
    IconButton(
      icon: Icon(Icons.search),
      onPressed: () {},
    ),
  ],
);
```
### Floating Action Button
```dart
FloatingActionButton(
  child: Icon(Icons.create),
  onPressed: () {},
);
```

### Drawer
```dart
// Drawer
Drawer(
  child: ListView(
    children: <Widget>[
      UserAccountsDrawerHeader(
        currentAccountPicture: CircleAvatar(
          child: Text('JD'),
        ),
        accountName: Text('John Doe'),
        accountEmail: Text('john.doe@example.com'),
      ),
      ListTile(
        leading: Icon(Icons.search),
        title: Text('Search'),
      ),
      ListTile(
        leading: Icon(Icons.history),
        title: Text('History'),
      ),
    ],
  ),
);
```

### Bottom App Bar
```dart
BottomAppBar(
  child: Text('Bottom'),
  color: Colors.red,
);
```

### Bottom Navigation Bar
```dart
 BottomNavigationBar(
  currentIndex: 1,
  type: BottomNavigationBarType.shifting,
  items: [
    BottomNavigationBarItem(
      icon: Icon(Icons.cake),
      title: Text('Cake'),
      backgroundColor: Colors.red.shade100,
    ),
    BottomNavigationBarItem(
      icon: Icon(Icons.map),
      title: Text('Map'),
      backgroundColor: Colors.green.shade100,
    ),
    BottomNavigationBarItem(
      icon: Icon(Icons.alarm),
      title: Text('Alarm'),
      backgroundColor: Colors.blue.shade100,
    ),
  ],
);

```

### Bottom Sheet
 
```dart
BottomSheet(
  onClosing: () {},
  builder: (context) {
    return Text('Bottom');
  },
);
 
```


### SnackBar
```dart
Scaffold.of(context).showSnackBar(SnackBar(
  content: Text('This is a message.'),
  action: SnackBarAction(label: 'OK', onPressed: () {}),
));
 
```


### Scaffolding iOS Pages
- Use CupertinoPageScaffold.
```dart
CupertinoPageScaffold(
  navigationBar: CupertinoNavigationBar(
    middle: Text('App'),
    trailing: CupertinoButton(
      child: Icon(CupertinoIcons.search),
      onPressed: () {},
    ),
 ),
  child: Container(),
);
```
 

