# 全选文本

```dart
_controller.selection = TextSelection(
    baseOffset: 0,
    extentOffset: textValue.length,
);
```

`extension`:

```dart
extension TextEditingControllerExt on TextEditingController {
  void selectAll() {
    if (text.isEmpty) return;
    
    selection = TextSelection(
    baseOffset: 0,
    extentOffset: text.length
    );
  }
}
```