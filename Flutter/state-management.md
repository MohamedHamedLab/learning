
# State Management


## Managing State Using Stateful Widgets
- StatefulWidget class is the fundamental way in Flutter to manage state.
- A stateful widget rebuilds itself when its state changes.

Lifecycle methods of State

- initState(): Called when this object is inserted into the widgets tree. Should be used to perform initialization of state.
- didChangeDependencies(): Called when a dependency of this object changes.
- didUpdateWidget(T oldWidget): Called when the widget of this object changes. Old widget is passed as a parameter.
- reassemble(): Called when the app is reassembled during debugging. This method is only called during development.
- build(BuildContext context): Called when the state changes.
- deactivate(): Called when this object is removed from the widgets tree.
- dispose(): Called when this object is removed from the widgets tree permanently. This method is called after deactivate().
  
```dart
 class SelectColor extends StatefulWidget {
  @override
  _SelectColorState createState() => _SelectColorState();
}
class _SelectColorState extends State<SelectColor> {
  final List<String> _colors = ['Red', 'Green', 'Blue'];
  String _selectedColor;
  @override
  Widget build(BuildContext context) {
    return Column(
      children: <Widget>[
        DropdownButton(
          value: _selectedColor,
          items: _colors.map((String color) {
            return DropdownMenuItem(
              value: color,
              child: Text(color),
            );
          }).toList(),
          onChanged: (value) {
            setState(() {
              _selectedColor = value;
            });
          },
        ),
        Text('Selected: ${_selectedColor ?? }'),
      ],
    );
    }
}

```
## Managing State Using Redux

```dart
 class JobsState extends Equatable {
  JobsState({bool loading, bool error, List<Job> data})
      : _loading = loading,
        _error = error,
        _data = data,
        super([loading, error, data]);
        final bool _loading;
        final bool _error;
        final List<Job> _data;
        bool get loading => _loading ?? false;
        bool get error => _error ?? false;
        List<Job> get data => _data ?? [];
        bool get empty => _loading == null && _error == null && _data == null;
        JobsState copyWith({bool loading, bool error, List<Job> data}) {
            return JobsState(
            loading: loading ?? this._loading,
            error: error ?? this._error,
            data: data ?? this._data,
            );
        }
    }
   abstract class JobsAction extends Equatable {
        JobsAction([List props = const []]) : super(props);
    }
    class LoadJobAction extends JobsAction {
    LoadJobAction({@required this.keyword})
        : assert(keyword != null),
            super([keyword]);
    final String keyword;
    }
    class JobLoadedAction extends JobsAction {
    JobLoadedAction({@required this.jobs})
        : assert(jobs != null),
            super([jobs]);
    final List<Job> jobs;
    }  

    JobsState jobsReducers(JobsState state, dynamic action) {
  if (action is LoadJobAction) {
    return state.copyWith(loading: true);
  } else if (action is JobLoadErrorAction) {
    return state.copyWith(loading: false, error: true);
  } else if (action is JobLoadedAction) {
    return state.copyWith(loading: false, data: action.jobs);
  }
  return state;
}   

ThunkAction<JobsState> getJobs(GitHubJobsClient jobsClient, String keyword) {
  return (Store<JobsState> store) async {
    store.dispatch(LoadJobAction(keyword: keyword));
    try {
      List<Job> jobs = await jobsClient.getJobs(keyword);
      store.dispatch(JobLoadedAction(jobs: jobs));
    } catch (e) {
      store.dispatch(JobLoadErrorAction());
    }
  };

  class GitHubJobs extends StatefulWidget {
  GitHubJobs({
    Key key,
    @required this.store,
    @required this.jobsClient,
  })  : assert(store != null),
        assert(jobsClient != null),
        super(key: key);
  final Store<JobsState> store;
  final GitHubJobsClient jobsClient;
  @override
  _GitHubJobsState createState() => _GitHubJobsState();
}
class _GitHubJobsState extends State<GitHubJobs> {
  @override
  Widget build(BuildContext context) {
    return StoreProvider<JobsState>(
      store: widget.store,
      child: Column(
        children: <Widget>[
          Padding(
            padding: const EdgeInsets.all(8.0),
            child: KeywordInput(
              jobsClient: widget.jobsClient,
            ),
            ),
          Expanded(
            child: JobsView(),
          ),
        ],
      ),
    );
  }
}
class KeywordInput extends StatefulWidget {
  KeywordInput({this.jobsClient});
  final GitHubJobsClient jobsClient;
  @override
  _KeywordInputState createState() => _KeywordInputState();
}
class _KeywordInputState extends State<KeywordInput> {
  final GlobalKey<FormFieldState<String>> _keywordFormKey = GlobalKey();
  @override
  Widget build(BuildContext context) {
    return Row(
      children: <Widget>[
        Expanded(
          child: TextFormField(
            key: _keywordFormKey,
          ),
        ),
        StoreBuilder<JobsState>(
          builder: (BuildContext context, Store<JobsState> store) {
            return IconButton(
              icon: Icon(Icons.search),
              onPressed: () {
                String keyword = _keywordFormKey.currentState?.value ?? "";
                if (keyword.isNotEmpty) {
                  store.dispatch(getJobs(widget.jobsClient, keyword));
                }
                              },
            );
          },
        ),
      ],
    );
  }
}
class JobsView extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return StoreConnector<JobsState, JobsState>(
      converter: (Store<JobsState> store) => store.state,
      builder: (BuildContext context, JobsState state) {
        if (state.empty) {
          return Center(
            child: Text('Input keyword and search'),
          );
        } else if (state.loading) {
          return Center(
            child: CircularProgressIndicator(),
          );
        } else if (state.error) {
          return Center(
            child: Text(
              'Failed to get jobs',
              style: TextStyle(color: Colors.red),
            ),
          );
        } else {
          return JobsList(state.data);
        }
      },
    );
  }
}

```
