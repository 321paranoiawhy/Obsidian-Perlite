## 频繁 setState

```dart
Timer.periodic(const Duration(microseconds: 1)
	() {
		setState(() {
			// do something
		});
	}
);
```

## 同步还是异步?

## 连续多次 setState

```dart
setState(() {
		// do something
	}
);

setState(() {
		// do something
	}
);

setState(() {
		// do something
	}
);
```



## 空 setState

```dart
setState(() {
		_time = DateTime.now();
	}
);
```

```dart
_time = DateTime.now();

setState(() {});
```

## 设置同一状态

```dart
setState(() {
		// 假定当前 _status == true
		// 此时 setState 什么也不做
		_status = true;
	}
);
```
