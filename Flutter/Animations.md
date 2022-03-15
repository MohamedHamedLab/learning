# Animations 

## Creating Simple Animations

```dart
 class GrowingImage extends StatefulWidget {
  @override
  _GrowingImageState createState() => _GrowingImageState();
}
class _GrowingImageState extends State<GrowingImage>
    with SingleTickerProviderStateMixin {
  AnimationController controller;
  @override
  void initState() {
    super.initState();
    controller = AnimationController(
      lowerBound: 0,
      upperBound: 400,
      duration: const Duration(seconds: 10),
      vsync: this,
    )
      ..addListener(() {
        setState(() {});
      })
      ..forward();
  }
  @override
  Widget build(BuildContext context) {
    return SizedBox(
      width: controller.value,
      height: controller.value,
      child: Image.network('https://picsum.photos/400'),
    );
  }
  @override
  void dispose() {
    controller.dispose();
    super.dispose();
  }
}
```

## Creating Animations Using Linear Interpolation
```dart
 class AnimatedColorTween extends StatefulWidget {
  @override
  _AnimatedColorTweenState createState() => _AnimatedColorTweenState();
}
class _AnimatedColorTweenState extends State<AnimatedColorTween>
    with SingleTickerProviderStateMixin {
  AnimationController controller;
  Animation<Color> animation;
  @override
  void initState() {
    super.initState();
    controller = AnimationController(
      duration: const Duration(seconds: 10),
      vsync: this,
    );
    animation =
        ColorTween(begin: Colors.red, end: Colors.green).animate(controller);
    controller.forward();
  }
  @override
  Widget build(BuildContext context) {
    return AnimatedColor(
      animation: animation,
    );
  }
  @override
  void dispose() {
    controller.dispose();
    super.dispose();
  }
}
class AnimatedColor extends AnimatedWidget {
  AnimatedColor({Key key, this.animation})
      : super(key: key, listenable: animation);
  final Animation<Color> animation;
  @override
  Widget build(BuildContext context) {
    return Container(
      width: 300,
      height: 300,
      decoration: BoxDecoration(color: animation.value),
    );
  }
}
```


## Creating Curved Animations

```dart
 class CurvedPosition extends StatefulWidget {
  @override
  _CurvedPositionState createState() => _CurvedPositionState();
}
class _CurvedPositionState extends State<CurvedPosition>
    with SingleTickerProviderStateMixin {
  AnimationController controller;
  Animation<double> animation;
  @override
  void initState() {
    super.initState();
    controller = AnimationController(
      duration: const Duration(seconds: 5),
      vsync: this,
    )..forward();
    animation = CurvedAnimation(parent: controller, curve: Curves.easeInOut);
    @override
  Widget build(BuildContext context) {
    return AnimatedBox(
      animation: animation,
    );
  }
  @override
  void dispose() {
    controller.dispose();
    super.dispose();
  }
  }
}
class AnimatedBox extends AnimatedWidget {
  AnimatedBox({Key key, this.animation})
      : super(key: key, listenable: animation);
  final Animation<double> animation;
  final double _width = 400;
  @override
  Widget build(BuildContext context) {
    return Container(
      width: _width,
      height: 20,
      child: Stack(
        children: <Widget>[
          Positioned(
            left: animation.value * _width,
            bottom: 0,
            child: Container(
              width: 10,
              height: 10,
              decoration: BoxDecoration(color: Colors.red),
            ),
          )
        ],
      ),
    );
  }
}
```

## Chaining Tweens

```dart
 var animation = Tween(begin: 0.0, end: 300.0)
  .chain(CurveTween(curve: Curves.easeOut))
  .animate(controller);
```

## Creating Sequences of Tweens

```dart
 var animation = TweenSequence([
  TweenSequenceItem(
    tween: Tween(begin: 0.0, end: 100.0),
    weight: 40,
  ),
  TweenSequenceItem(
    tween: Tween(begin: 100.0, end: 300.0)
        .chain(CurveTween(curve: Curves.easeInOut)),
    weight: 60,
  )
]).animate(controller);
```
