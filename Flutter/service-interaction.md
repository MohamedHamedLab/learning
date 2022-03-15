# Service Interaction

## Futures
-  interaction with backend services.
- `Future<T>` class from `dart:async` library is a representation of delayed computations.
- When given a Future object, you can register callbacks to handle the value or error once it is available.

 there are three different cases regarding its result:
* The computation never completes. No callbacks will be invoked.
* The computation completes with a value. Value callbacks are invoked with the value.
* The computation completes with an error. Error callbacks are invoked with the error.

```dart
Future.delayed(
  Duration(seconds: 1),
  () {
    if (Random().nextBool()) {
      return 1;
    } else {
      throw Error();
    }
  },
).then((value) {
  print(value);
}).catchError((error) {
  print('error: $error');
});

// other example 
Future.value(1)
  .then((value) => value + 1)
  .then((value) => value * 10)
  .then((value) => value + 2)
  .then((value) => print(value));

//exmple 3
Future.value(1).then((value) {
  print(value);
}).whenComplete(() {
  print('complete');
});
```

## Using async and await to Work with Futures
```dart
Future<int> getValue() {
  return Future.value(1);
}
Future<int> calculate() async {
  int value = await getValue();
  return value * 10;
}

// futuer with error 
Future<int> getErrorValue() {
  return Future.error('invalid value');
}
Future<int> calculateWithError() async {
  try {
    return await getErrorValue();
  } catch (e) {
    print(e);
    return 1;
    } finally {
    print('done');
  }
}
```


## Working with Streams
There can be three types of events in a stream:
- Data event represents actual data in the stream. These events are also called elements in the stream.
- Error event represents errors occurred.
- Done event represents that the end of stream has reached. No more events will be emitted.

there are different Stream constructors to create Stream objects:
- Stream.empty() constructor creates an empty broadcast stream.
- Stream.fromFuture() constructor creates a single-subscription stream from a Future object.
- Stream.fromFutures() constructor creates a stream from a list of Future objects.
- Stream.fromInterable() constructor creates a single-subscription stream from elements of an Iterable object.
- Stream.periodic() constructor creates a stream that periodically emits data events at the given intervals.


```dart
 Stream.fromIterable([1, 2, 3]).listen(
  (value) => print(value),
  onError: (error) => print('error: $error'),
  onDone: () => print('done'),
  cancelOnError: true,
);
// Stream Transformation

Stream.fromIterable([1, 2, 3]).asyncExpand((int value) {
  return Stream.fromIterable([value * 5, value * 10]);
}).listen(print);
// -> 5, 10, 10, 20, 15, 30
Stream.fromIterable([1, 2, 3]).expand((int value) {
  return [value * 5, value * 10];
}).listen(print);
// -> 5, 10, 10, 20, 15, 30
Stream.fromIterable([1, 2, 3]).asyncMap((int value) {
  return Future.delayed(Duration(seconds: 1), () => value * 10);
}).listen(print);
// -> 10, 20, 30
Stream.fromIterable([1, 2, 3]).map((value) => value * 10).listen(print);
// -> 10, 20, 30
Stream.fromIterable([1, 1, 2]).distinct().listen(print);
// -> 1, 2
Stream.fromIterable([1, 2, 3]).skip(1).listen(print);
// -> 2, 3
Stream.fromIterable([1, 2, 3])
    .skipWhile((value) => value % 2 == 1)
    .listen(print);
// -> 2, 3
Stream.fromIterable([1, 2, 3]).take(1).listen(print);
// -> 1
Stream.fromIterable([1, 2, 3])
    .takeWhile((value) => value % 2 == 1)
    .listen(print);
// -> 1
Stream.fromIterable([1, 2, 3]).where((value) => value % 2 == 1).listen(print);
// -> 1, 3
Stream.fromIterable([1, 2, 3]).forEach(print);
// -> 1, 2, 3
Stream.fromIterable([1, 2, 3]).contains(1).then(print);
// -> true
Stream.fromIterable([1, 2, 3]).any((value) => value % 2 == 0).then(print);
// -> true
Stream.fromIterable([1, 2, 3]).every((value) => value % 2 == 0).then(print);
// -> false
Stream.fromIterable([1, 2, 3]).fold(0, (v1, v2) => v1 + v2).then(print);
// -> 6
Stream.fromIterable([1, 2, 3]).reduce((v1, v2) => v1 * v2).then(print);
// -> 6
Stream.fromIterable([1, 2, 3])
    .firstWhere((value) => value % 2 == 1)
    .then(print);
// -> 1
Stream.fromIterable([1, 2, 3])
    .lastWhere((value) => value % 2 == 1)
    .then(print);
// -> 3
Stream.fromIterable([1, 2, 3])
    .singleWhere((value) => value % 2 == 1)
    .then(print);
// -> Unhandled exception: Bad state: Too many elements
```

## Handle Simple JSON Data

```dart
 var data = {
  'name': 'Test',
  'count': 100,
  'valid': true,
  'list': [
    1,
    2,
    {
      'nested': 'a',
      'value': 123,
    },
  ],
};
String str = jsonEncode(data);
print(str);
```

## Connecting to WebSocket

```dart
 WebSocket.connect('ws://demos.kaazing.com/echo').then((WebSocket webSocket) {
  webSocket.listen(print, onError: print);
  webSocket.add('hello');
  webSocket.add('world');
  webSocket.close();
}).catchError(print);

// connect to socket servers

import 'dart:io';
import 'dart:convert';
void main() {
  ServerSocket.bind('127.0.0.1', 10080).then((serverSocket) {
    serverSocket.listen((socket) {
      socket.addStream(socket
          .transform(utf8.decoder)
          .map((str) => str.toUpperCase())
          .transform(utf8.encoder));
    });
  });
}

//  connect to the socket server 
void main() {
  Socket.connect('127.0.0.1', 10080).then((socket) {
    socket.transform(utf8.decoder).listen(print);
    socket.write('hello');
    socket.write('world');
    socket.close();
  });
}

```
## Interacting JSON-Based REST Services

```dart
 class GitHubJobsPage extends StatelessWidget {
  final Future<List<Job>> _jobs = HttpClient()
      .getUrl(Uri.parse('https://jobs.github.com/positions.json'
          '?description=java&location=new+york'))
      .then((HttpClientRequest request) => request.close())
      .then((HttpClientResponse response) {
    return response.transform(utf8.decoder).join("").then((String content) {
      return (jsonDecode(content) as List<dynamic>)
          .map((json) => Job.fromJson(json))
          .toList();
    });
  });

@override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('GitHub Jobs'),
      ),
      body: FutureBuilder<List<Job>>(
        future: _jobs,
        builder: (BuildContext context, AsyncSnapshot<List<Job>> snapshot) {
          if (snapshot.hasData) {
            return JobsList(snapshot.data);
            } else if (snapshot.hasError) {
            return Center(
              child: Text(
                '${snapshot.error}',
                style: TextStyle(color: Colors.red),
              ),
            );
          } else {
            return Center(
              child: CircularProgressIndicator(),
            );
          }
        },
      ),
    );
  }
}

class JobsList extends StatelessWidget {
  JobsList(this.jobs);
  final List<Job> jobs;
  @override
  Widget build(BuildContext context) {
    return ListView.separated(
      itemBuilder: (BuildContext context, int index) {
        Job job = jobs[index];
        return ListTile(
          title: Text(job.title),
          subtitle: Text(job.company),
        );
      },
      separatorBuilder: (BuildContext context, int index) {
        return Divider();
      },
      itemCount: jobs.length,
    );
  }
}
```




```dart
 
```

