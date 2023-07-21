`ValueListenableBuilder` 通过监听数据源, 仅当数据源发生变化时, 会重新执行其 `builder`:

```dart
// webview 加载进度
final ValueNotifier<int> _loadingPercentage = ValueNotifier(0);

Stack(children: [
	WebView(
		initialUrl: widget.lifeSmartURL,
		javascriptMode: JavascriptMode.unrestricted,
		onProgress: (int progress) {
	    _loadingPercentage.value = progress;
    },
    onPageFinished: (String url) {
	    _loadingPercentage.value = 100;
    },
  ),
  ValueListenableBuilder(
      valueListenable: _loadingPercentage,
      builder: (BuildContext context, int value, Widget? child) {
        return Offstage(
	        offstage: value >= 100,
          child: LinearProgressIndicator(
	          value: value / 100.0,
          ),
        );
		  },
	),
])
```

如果不使用 `Offstage` 包裹 `LinearProgressIndicator`, 而使用 `if (_loadingPercentage.value < 100)`, 则在 `onPageFinished` 中须手动调用 `setState`:

```dart
Stack(children: [
	WebView(
		initialUrl: widget.lifeSmartURL,
		javascriptMode: JavascriptMode.unrestricted,
		onProgress: (int progress) {
	    _loadingPercentage.value = progress;
    },
    onPageFinished: (String url) {
	    _loadingPercentage.value = 100;
	    setState(() {});
    },
  ),
  if (_loadingPercentage.value < 100)
	  ValueListenableBuilder(
	    valueListenable: _loadingPercentage,
	    builder: (BuildContext context, int value, Widget? child) {
	      return LinearProgressIndicator(
		      value: value / 100.0,
	      );
			},
		),
])
```

- [按需rebuild（ValueListenableBuilder]([7.5 按需rebuild（ValueListenableBuilder） | 《Flutter实战·第二版》 (flutterchina.club)](https://book.flutterchina.club/chapter7/value_listenable_builder.html#_7-5-2-%E5%AE%9E%E4%BE%8B))

## ValueListenable

- [ValueListenable\<T> class](https://api.flutter.dev/flutter/foundation/ValueListenable-class.html)

```dart
const ValueListenableBuilder({
  Key? key,
  required this.valueListenable, // 数据源，类型为 ValueListenable<T>
  required this.builder, // builder
  this.child,
}
```

- `valueListenable`, 表示一个可监听的数据源
- `builder`, 类型为 `Widget Function(BuildContext context, int value, Widget? child)`
- `child`, 不可变组件, 可作为缓存项传入 `builder` 的第三个入参 `Widget? child`
