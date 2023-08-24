# CustomPainter

- [flutter_dash](https://pub.dev/packages/flutter_dash)

## Dashed Line

### HorizontalDashedLinePainter

```dart
import 'package:flutter/material.dart';

@immutable
class HorizontalDashedLinePainter extends CustomPainter {
  final double dashWidth;
  final double dashHeight;
  final double dashGap;
  final Color dashColor;

  const HorizontalDashedLinePainter(
      {required this.dashWidth,
      required this.dashHeight,
      required this.dashGap,
      required this.dashColor});

  @override
  void paint(Canvas canvas, Size size) {
    double startX = 0;

    final paint = Paint()
      ..color = dashColor
      ..strokeWidth = dashHeight;

    while (startX < size.width) {
      canvas.drawLine(Offset(startX, 0), Offset(startX + dashWidth, 0), paint);
      startX += dashWidth + dashGap;
    }
  }

  @override
  bool shouldRepaint(CustomPainter oldDelegate) => false;
}
```

### VerticalDashedLinePainter

```dart
import 'package:flutter/material.dart';

@immutable
class VerticalDashedLinePainter extends CustomPainter {
  final double dashWidth;
  final double dashHeight;
  final double dashGap;
  final Color dashColor;

  const VerticalDashedLinePainter(
      {required this.dashWidth,
      required this.dashHeight,
      required this.dashGap,
      required this.dashColor});

  @override
  void paint(Canvas canvas, Size size) {
    double startY = 0;

    final paint = Paint()
      ..color = dashColor
      ..strokeWidth = dashWidth;

    while (startY < size.height) {
      canvas.drawLine(Offset(0, startY), Offset(0, startY + dashHeight), paint);
      startY += dashHeight + dashGap;
    }
  }

  @override
  bool shouldRepaint(CustomPainter oldDelegate) => false;
}
```

### 使用 `StatelessWidget` 封装成组件

`DashedLine`:

```dart
import 'package:flutter/material.dart';

enum LineDirection {
  horizontal,
  vertical,
}

@immutable
class DashedLine extends StatelessWidget {
  final double dashWidth;
  final double dashHeight;
  final double dashGap;
  final Color dashColor;
  final LineDirection direction;
  final Widget child;
  const DashedLine(
      {this.dashWidth = 5,
      this.dashHeight = 1,
      this.dashGap = 5,
      this.dashColor = Colors.grey,
      this.direction = LineDirection.horizontal,
      required this.child,
      super.key});

  @override
  Widget build(BuildContext context) {
    return CustomPaint(
        painter: switch (direction) {
      LineDirection.horizontal => HorizontalDashedLinePainter(
          dashWidth: dashWidth,
          dashHeight: dashHeight,
          dashGap: dashGap,
          dashColor: dashColor),
      LineDirection.vertical => VerticalDashedLinePainter(
          dashWidth: dashWidth,
          dashHeight: dashHeight,
          dashGap: dashGap,
          dashColor: dashColor),
		    },
		    child: child,
    );
  }
}
```

## DottedLine

### HorizontalDottedLine

```dart
import 'package:flutter/material.dart';

@immutable
class HorizontalDottedLinePainter extends CustomPainter {
  final double dotRadius;
  final double dotGap;
  final Color dotColor;

  const HorizontalDottedLinePainter(
      {required this.dotRadius, required this.dotGap, required this.dotColor});

  @override
  void paint(Canvas canvas, Size size) {
    double startX = 0;

    final paint = Paint()
      ..color = dotColor
      ..style = PaintingStyle.fill;

    while (startX < size.width) {
      canvas.drawCircle(Offset(startX + dotRadius, 0), dotRadius, paint);
      startX += dotRadius + dotGap;
    }
  }

  @override
  bool shouldRepaint(CustomPainter oldDelegate) => false;
}
```

### VerticalDottedLine

```dart
import 'package:flutter/material.dart';

@immutable
class VerticalDottedLinePainter extends CustomPainter {
  final double dotRadius;
  final double dotGap;
  final Color dotColor;

  const VerticalDottedLinePainter(
      {required this.dotRadius, required this.dotGap, required this.dotColor});

  @override
  void paint(Canvas canvas, Size size) {
    double startY = 0;

    final paint = Paint()
      ..color = dotColor
      ..style = PaintingStyle.fill;

    while (startY < size.height) {
      canvas.drawCircle(Offset(0, startY + dotRadius), dotRadius, paint);
      startY += dotRadius + dotGap;
    }
  }

  @override
  bool shouldRepaint(CustomPainter oldDelegate) => false;
}
```

### 使用 `StatelessWidget` 封装成组件

`DottedLine`:

```dart
import 'package:flutter/material.dart';

@immutable
class DottedLine extends StatelessWidget {
  final double dotRadius;
  final double dotGap;
  final Color dotColor;
  final LineDirection direction;
  final Widget child;
  const DottedLine(
      {this.dotRadius = 5,
      this.dotGap = 5,
      this.dotColor = Colors.grey,
      this.direction = LineDirection.horizontal,
      required this.child,
      super.key});

  @override
  Widget build(BuildContext context) {
    return CustomPaint(
        painter: switch (direction) {
      LineDirection.horizontal => HorizontalDottedLinePainter(
          dotRadius: dotRadius, dotGap: dotGap, dotColor: dotColor),
      LineDirection.vertical => VerticalDottedLinePainter(
          dotRadius: dotRadius, dotGap: dotGap, dotColor: dotColor),
		    },
		    child: child,
    );
  }
}
```
