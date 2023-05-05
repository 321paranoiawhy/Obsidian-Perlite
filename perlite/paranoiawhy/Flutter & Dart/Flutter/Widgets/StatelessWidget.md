# `StatelessWidget` 内保存/刷新状态

使用 `StatefullBuilder`:

```dart
AlertDialog(
	content: StatefulBuilder(  
		builder: (BuildContext context, StateSetter setState) {
			
		}
	)
);

showDialog(
	context: context,
	barrierDismissible: false,
	builder: (context) => StatefulBuilder(
	    builder: (BuildContext context, StateSetter setState) {
		    return AlertDialog();
	    }
	 )
);
```

# 传参

```dart
class Example extends StatelessWidget {
  final String title;
  final VoidCallback onPressed;
  const Example({Key? key, required this.title, required this.onPressed}) : super(key: key);

	@override
	Widget build(BuildContext context) {
		return Text('Example');
	}
}
```