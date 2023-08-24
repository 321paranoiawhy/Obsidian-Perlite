## circle_loading

- [How to draw and animate designs with Flutter CustomPaint Widget](https://blog.codemagic.io/flutter-custom-painter/)

```dart
import 'dart:math';

import 'package:flutter/material.dart';

class CircleLoading extends StatefulWidget {
  /// 一次完整的动画时间
  final Duration duration;

  final Widget? child;

  /// 圆形背景色
  final Color backgroundColor;

  const CircleLoading(
      {this.duration = const Duration(seconds: 2),
      this.child,
      this.backgroundColor = Colors.teal,
      Key? key})
      : super(key: key);

  @override
  State<CircleLoading> createState() => _CircleLoadingState();
}

class _CircleLoadingState extends State<CircleLoading>
    with TickerProviderStateMixin {
  late Animation<double> _animation;
  late AnimationController _controller;
  final Tween<double> _rotationTween = Tween(begin: -pi, end: pi);

  @override
  void initState() {
    super.initState();

    _controller = AnimationController(
      vsync: this,
      duration: widget.duration,
    );

    _animation = _rotationTween.animate(_controller)
      ..addListener(() {
        setState(() {});
      })
      ..addStatusListener((AnimationStatus status) {
        if (status == AnimationStatus.completed) {
          _controller.repeat();
        } else if (status == AnimationStatus.dismissed) {
          _controller.forward();
        }
      });

    _controller.forward();
  }

  @override
  void dispose() {
    _controller.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Transform.rotate(
      angle: _animation.value,
      child: CustomPaint(
        size: Size(18, 18),
        painter: CircleLoadingPainter(backgroundColor: widget.backgroundColor),
        child: widget.child,
      ),
    );
  }
}

class CircleLoadingPainter extends CustomPainter {
  final Color backgroundColor;
  CircleLoadingPainter({required this.backgroundColor});

  @override
  void paint(Canvas canvas, Size size) {
    /// 假设 size.width == size.height
    /// 否则为 椭圆
    final width = size.width;
    final height = size.height;
    final maxRadius = min(width, height) / 8;

    final Paint paint = Paint()
      ..color = backgroundColor
      ..style = PaintingStyle.fill
      ..strokeCap = StrokeCap.round;

    List<double> _radiusList = [
      8 * maxRadius / 8,
      1 * maxRadius / 8,
      2 * maxRadius / 8,
      3 * maxRadius / 8,
      4 * maxRadius / 8,
      5 * maxRadius / 8,
      6 * maxRadius / 8,
      7 * maxRadius / 8
    ];

    /// top
    Offset p0 = Offset(width / 2, 0 + _radiusList[0]);

    /// top right
    Offset p1 = Offset(width / 2 + sqrt(2) * (width - _radiusList[1]) / 4,
        height / 2 - sqrt(2) * (height - _radiusList[1]) / 4);

    /// right
    Offset p2 = Offset(width - _radiusList[2], height / 2);

    /// bottom right
    Offset p3 = Offset(width / 2 + sqrt(2) * (width - _radiusList[3]) / 4,
        height / 2 + sqrt(2) * (height - _radiusList[3]) / 4);

    /// bottom
    Offset p4 = Offset(width / 2, height - _radiusList[4]);

    /// bottom left
    Offset p5 = Offset(width / 2 - sqrt(2) * (width - _radiusList[5]) / 4,
        height / 2 + sqrt(2) * (height - _radiusList[5]) / 4);

    /// left
    Offset p6 = Offset(0 + _radiusList[6], height / 2);

    /// top left
    Offset p7 = Offset(width / 2 - sqrt(2) * (width - _radiusList[7]) / 4,
        height / 2 - sqrt(2) * (height - _radiusList[7]) / 4);

    List<Offset> _offsetList = [p0, p1, p2, p3, p4, p5, p6, p7];

    for (int index = 0; index < 8; index++) {
      canvas.drawCircle(_offsetList[index], _radiusList[index], paint);
    }

    // canvas
    //   ..drawLine(Offset.zero, Offset(width, 0), paint)
    //   ..drawLine(Offset(width, 0), Offset(width, height), paint)
    //   ..drawLine(Offset(width, height), Offset(0, height), paint)
    //   ..drawLine(Offset(0, height), Offset.zero, paint);

    // canvas.drawLine(startingPoint, endingPoint, paint);

    // canvas
    //   ..drawLine(startingPoint, endingPoint, paint)
    //   ..drawLine(startingPoint, endingPoint, paint);
  }

  @override
  bool shouldRepaint(CustomPainter oldDelegate) {
    return false;
  }
}
```

`canvas` 坐标原点在左上角, 向右为 `x` 轴正方向, 向下为 `y` 轴正方向。 

`drawLine` 语法:

```dart
// startPoint 起始点, endPoint 终止点
canvas.drawLine(startPoint, endPoint, paint);
```

`drawLine` 链式写法:

```dart
canvas
  ..drawLine(startPoint, endPoint, paint)
  ..drawLine(startPoint, endPoint, paint);
```

## step_loading

```dart
import 'package:flutter/material.dart';

class StepLoading extends StatefulWidget {
  /// 一次完整的动画时间
  final Duration duration;

  /// 透明度过渡动画时间
  final Duration opacityDuration;

  /// 当前小圆点数量
  final int dotCount;

  /// 小圆点大小
  final double? dotSize;

  /// 小圆点间距
  final double? dotGap;

  /// 小圆点背景色
  final Color backgroundColor;

  const StepLoading(
      {this.duration = const Duration(seconds: 2),
      this.opacityDuration = const Duration(milliseconds: 200),
      this.dotCount = 3,
      this.dotSize,
      this.dotGap,
      this.backgroundColor = const Color.fromRGBO(4, 4, 5, 1),
      Key? key})
      : super(key: key);

  @override
  State<StepLoading> createState() => _StepLoadingState();
}

class _StepLoadingState extends State<StepLoading>
    with TickerProviderStateMixin {
  late Animation<double> _animation;
  late AnimationController _controller;
  late final Tween<double> _rotationTween;

  @override
  void initState() {
    super.initState();

    _controller = AnimationController(
      vsync: this,
      duration: widget.duration,
    );

    _rotationTween = Tween(begin: 0, end: widget.dotCount.toDouble());

    _animation = _rotationTween.animate(_controller)
      ..addListener(() {
        setState(() {});
      })
      ..addStatusListener((AnimationStatus status) {
        if (status == AnimationStatus.completed) {
          _controller.repeat();
        } else if (status == AnimationStatus.dismissed) {
          _controller.forward();
        }
      });

    _controller.forward();
  }

  @override
  void dispose() {
    _controller.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Row(
      mainAxisAlignment: MainAxisAlignment.center,
      children: [
        for (int index = 0; index < widget.dotCount; index++)
          AnimatedOpacity(
            duration: widget.opacityDuration,
            opacity: _animation.value <= index ? 0 : 1,
            child: Container(
              width: widget.dotSize ?? 3,
              height: widget.dotSize ?? 3,
              margin: EdgeInsets.only(
                  right: index == widget.dotCount - 1
                      ? 0
                      : (widget.dotGap ?? 5)),
              decoration: BoxDecoration(
                  shape: BoxShape.circle, color: widget.backgroundColor),
            ),
          )
      ],
    );
  }
}
```
