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