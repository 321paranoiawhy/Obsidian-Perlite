- [WillPopScope class](https://api.flutter.dev/flutter/widgets/WillPopScope-class.html)

```dart
WillPopScope(
	onWillPop: () async {
		return true;
		// return false;
	},
	child: ...
```

- `WillPopScope` 可用于拦截**物理导航按钮**返回事件, 可用于防止用户误触而返回上一页或
- `onWillPop` 接收一个返回 `bool` 值的 `Future` 对象, 当返回 `true` 时, 允许返回上一页, 否则不返回。
- `child` 参数为任意 `Widget`

`Android` 和 `iOS` 平台差异可按如下方式解决:

```dart
// Platform.isIOS
GestureDetector(
	onPanUpdate: (DragUpdateDetails details) {
		if (details.delta.dx > 0) {
			// do something
			Navigator.of(context).pop();
		}
	},
	child: WillPopScope(
		onWillPop: () async {
			return false;
		},
		child: ...

// Platform.isAndroid
WillPopScope(
	onWillPop: () async {
		return true;
		// return false;
	},
	child: ...
```
