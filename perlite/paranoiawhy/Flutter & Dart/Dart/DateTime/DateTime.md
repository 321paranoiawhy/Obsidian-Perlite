# `parse`

[parse static method](https://api.flutter.dev/flutter/dart-core/DateTime/parse.html)

```dart
DateTime parse(String formattedString)
```

将字符串转换为 `DateTime`:

```dart
 // 结果均为 DateTime 标准格式 2023-01-06 00:00:00.000
DateTime.parse("2023-01-06");
DateTime.parse("20230106");
DateTime.parse("+20230106");

DateTime.parse("2023-01-06 00:00:00");
DateTime.parse("2023-01-06 00:00:00.000");
```

# `tryParse`

[tryParse static method](https://api.flutter.dev/flutter/dart-core/DateTime/tryParse.html)

```dart
DateTime? tryParse(String formattedString)
```

将字符串转换为 `DateTime`, 如果转换过程中有错误则返回 `null`:

```dart
static DateTime? tryParse(String formattedString) { 
// TODO: Optimize to avoid throwing. 
	try { 
		return parse(formattedString); 
	} on FormatException { 
		return null; 
	} 
}
```

# `millisecondsSinceEpoch`

[millisecondsSinceEpoch property](https://api.flutter.dev/flutter/dart-core/DateTime/millisecondsSinceEpoch.html)

```dart
external int get millisecondsSinceEpoch;
```

返回 `DateTime` 对应的 `Unix` 毫秒时间戳:

```dart
DateTime.parse("2023-01-06").millisecondsSinceEpoch; // 1672934400000
```

与之对应的 `microsecondsSinceEpoch`:

```dart
DateTime.parse("2023-01-06").microsecondsSinceEpoch; // 1672934400000000
```

# `fromMillisecondsSinceEpoch`

[DateTime.fromMillisecondsSinceEpoch constructor](https://api.flutter.dev/flutter/dart-core/DateTime/DateTime.fromMillisecondsSinceEpoch.html)

```dart
DateTime.fromMillisecondsSinceEpoch(
	int millisecondsSinceEpoch,
	{bool isUtc = false}
)
```

将毫秒时间戳转成 `DateTime`:

```dart
DateTime.fromMillisecondsSinceEpoch(1672934400000); // 2023-01-06 00:00:00.000
```

与之对应的 `fromMicrosecondsSinceEpoch`:

```dart
DateTime.fromMillisecondsSinceEpoch(1672934400000000); // 2023-01-06 00:00:00.000
```

# `DateTimeRange`

```dart
DateTimeRange({
	required this.start,
	required this.end, 
}) : assert(start != null),
	 assert(end != null),
	 assert(!start.isAfter(end));
```

```dart
DateTimeRange dateTimeRange = DateTimeRange("2023-01-06", "2023-01-07");
dateTimeRange.start; // 
dateTimeRange.end; // 
```

## `showDateRangePicker`

* [showDateRangePicker](https://api.flutter.dev/flutter/material/showDateRangePicker.html)
* [DatePicker, DateRangePicker, TimePicker](https://medium.com/flutter-taipei/%E4%BE%86%E5%90%A7-flutter-12-datepicker-daterangepicker-timepicker-f3c5ac473865)

```dart
DateTimeRange? range = await showDateRangePicker(
	context: context,
	initialDate: DateTime.now(), // 初始时间
	firstDate: DateTime(2023, 01), // 开始时间, 不能选择此前的时间
	lastDate: DateTime(2100, 12) // 结束时间, 不能选择此后的时间
);
```