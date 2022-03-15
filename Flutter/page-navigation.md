# Page Navigation

## Simple Navigation
```dart
 class SimpleNavigationPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Simple Navigation'),
      ),
      body: Center(
        child: RaisedButton(
          child: Text('Show page'),
          onPressed: () {
            Navigator.of(context).push(MaterialPageRoute(builder: (context) {
              return Scaffold(
                appBar: AppBar(
                  title: Text('New Page'),
                ),
                body: Center(
                  child: Column(
                    crossAxisAlignment: CrossAxisAlignment.center,
                    children: <Widget>[
                      Text('A new page'),
                      RaisedButton(
                        child: Text('Go back'),
                        onPressed: () {
                          Navigator.of(context).pop();
                        },
                      ),
                    ],
                  ),
                ),
              );
            }));
          },
          ),
      ),
    );
  }
}
```
## Using Named Routes
```dart
 class LogInPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
        appBar: AppBar(
        title: Text('Log In'),
      ),
      body: Center(
        child: RaisedButton(
          child: Text('Sign Up'),
          onPressed: () {
            Navigator.pushNamed(context, '/sign_up');
          },
        ),
      ),
    );
  }
}

class PageNavigationApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Page Navigation',
      home: IndexPage(),
      routes: {
        '/sign_up': (context) => SignUpPage(),
        '/log_in': (context) => LogInPage(),
      },
    );
  }
}

```

## Passing Data Between Routes

```dart
 class UserDetails {
  UserDetails(this.firstName, this.lastName);
  final String firstName;
  final String lastName;
}
class UserDetailsPage extends StatefulWidget {
  @override
  _UserDetailsPageState createState() => _UserDetailsPageState();
}
class _UserDetailsPageState extends State<UserDetailsPage> {
  UserDetails _userDetails = UserDetails('John', 'Doe');
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
          title: Text('User Details'),
      ),
      body: Column(
        children: <Widget>[
          Text('First name: ${_userDetails.firstName}'),
          Text('Last name: ${_userDetails.lastName}'),
          RaisedButton.icon(
            label: Text('Edit (route builder)'),
            icon: Icon(Icons.edit),
            onPressed: () async {
              UserDetails result = await Navigator.push(
                context,
                MaterialPageRoute<UserDetails>(
                  builder: (BuildContext context) {
                    return EditUserDetailsPage(_userDetails);
                  },
                ),
              );
              if (result != null) {
                setState(() {
                  _userDetails = result;
                });
              }
            },
          ),
        ],
      ),
    );
  }
}
```



## iOS Action Sheets

```dart
 
```





```dart
 CupertinoButton(
  child: Text('Show Action Sheet'),
  onPressed: () async {
    String result = await showCupertinoModalPopup<String>(
      context: context,
      builder: (BuildContext context) {
        return CupertinoActionSheet(
          title: Text('What to do'),
          message: Text('Please select an action'),
          actions: <Widget>[
            CupertinoActionSheetAction(
              child: Text('Duplicate'),
              isDefaultAction: true,
              onPressed: () {
                Navigator.pop(context, 'duplicate');
              },
            ),
            CupertinoActionSheetAction(
              child: Text('Move'),
              onPressed: () {
                Navigator.pop(context, 'move');
              },
            ),
            CupertinoActionSheetAction(
              isDestructiveAction: true,
              child: Text('Delete'),
              onPressed: () {
                Navigator.pop(context, 'delete');
              },
            ),
          ],
          cancelButton: CupertinoActionSheetAction(
            child: Text('Cancel'),
            onPressed: () {
              Navigator.pop(context);
            },
          ),
        );
      },
         );
    print(result);
  },
);
```