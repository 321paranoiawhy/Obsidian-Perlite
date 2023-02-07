# `Future.wait`

[wait](https://api.dart.dev/stable/2.18.6/dart-async/Future/wait.html)

并发请求:

```dart
Future<String> firstAsync() async {
	await Future.delayed(const Duration(seconds: 1));
	print("First");
	return "First";
}

Future<String> secondAsync() async {
	await Future.delayed(const Duration(seconds: 1));
	print("Second");
	return "Second";
}

Future<String> thirdAsync() async {
	await Future.delayed(const Duration(seconds: 1));
	print("Third");
	return "Third";
}

void main() async {
	int start = DateTime.now().millisecondsSinceEpoch;
	List result = await Future.wait([firstAsync(), secondAsync(), thirdAsync()]);
	print(result); // ["First", "Second", "Third"]
	int end = DateTime.now().millisecondsSinceEpoch;
	print("${end - start} ms"); // 1007 ms
}
```

# `Future.forEach`

[forEach](https://api.dart.dev/stable/2.18.6/dart-async/Future/forEach.html)
[future_forEach - Gist](https://gist.github.com/Hasilt/8d0584ac8ae2c8e5e147946cca0e0498)

依次请求:

```dart
Future<int> waitForOneSecond(int value) async {
	await Future.delayed(const Duration(seconds: 1));
	print(value);
	return value;
}

void main() async {
	int start = DateTime.now().millisecondsSinceEpoch;
	List _result = [];
	await Future.forEach([0, 1, 2], (value) async {
		int result = await waitForOneSecond(value);
		_result.add(result);
	});
	print(_result); // [0, 1, 2]
	int end = DateTime.now().millisecondsSinceEpoch;
	print("${end - start} ms"); // 3033 ms
}
```

# `Future.sync`

[Future.sync constructor](https://api.flutter.dev/flutter/dart-async/Future/Future.sync.html)

立即执行的异步任务:

```dart
// "start" -> "first" -> "end" -> "second"
void main() {
	print("start"); // 1
	Future.sync((){ print("first"); }); // 2
	Future((){ print("second"); }); // 4
	print("end"); // 3
}
```

# `timeout`

[timeout method](https://api.dart.dev/stable/2.18.6/dart-async/Future/timeout.html)

```dart
void main() {
	Future((){ print("future"); }).timeout(
		const Duration(seconds: 1),
		onTimeout: () { print("timeout"); }
	); // "future"

	Future.delayed(const Duration(seconds: 1)).timeout(const Duration(seconds: 1),
      onTimeout: () {
    print("timeout");
  }); // nothing happens

	Future.delayed(const Duration(seconds: 2)).timeout(const Duration(seconds: 1),
      onTimeout: () {
    print("timeout");
  }); // timeout
}
```