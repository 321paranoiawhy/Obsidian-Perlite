#TextField
# `controller`

[TextEditingController class - api.dart.dev](https://api.flutter.dev/flutter/widgets/TextEditingController-class.html)

```dart
// 定义一个 TextEditingController
TextEditingController inputController = TextEditingController();

// 使用 inputController 作为 TextField 的 controller
TextField(controller: inputController)

// 清空输入框
inputController.clear();
// (getter) 获取输入框的值 (String 类型)
// https://api.flutter.dev/flutter/widgets/TextEditingController/text.html
inputController.text;
// (setter) 赋值 (如初始值、中间值)
inputController.text = "initial value";
// 获取选中的值
// https://api.flutter.dev/flutter/widgets/TextEditingController/selection.html
inputController.selection;
```

# `focusNode`

```dart
// 定义一个 FocusNode
FocusNode inputFocusNode = FocusNode();

// 使用 inputFocusNode 作为 TextField 的 focusNode
TextField(focusNode: inputFocusNode)

// 聚焦至当前输入框
inputFocusNode.requestFocus();
```

# `textAlign`

`textAlign` 类型为 `TextAlign`, 枚举值:

- `left`, 文字默认对齐方式
- `right`
- `center`
- `justify`
- `start`
- `end`

## `keyboardType`

`keyboardType` 类型为 `TextInputType`, 枚举值:

- `text`, 实现为 `TextInputType._(0)`
- `multiline`, 实现为 `TextInputType._(1)`
- `number`, 实现为 `TextInputType.numberWithOptions()`
- `phone`, 实现为 `TextInputType._(3)`
- `datetime`, 实现为 `TextInputType._(4)`
- `emailAddress`, 实现为 `TextInputType._(5)`
- `url`, 实现为 `TextInputType._(6)`
- `visiblePassword`, 实现为 `TextInputType._(7)`

# `textDirection`

`textDirection` 类型为 TextDirection`, 枚举值为:

- `ltr`, left to right, 文字方向从左至右
- `rtl`, right to left, 文字方向从右至左

# 文字垂直居中

```dart
decoration: InputDecoration(
	contentPadding: EdgeInsets.zero,
),
```

# 限制最大输入长度

```dart
// 限制最大输入长度为 10
inputFormatters: [LengthLimitingTextInputFormatter(10)],
```

# 计算当前行数



给 `TextField` 一个 `inputKey`, 在 `TextField` 的 `onChanged` 回调里调用:

```dart
String text = 'Example text.';

final TextSpan textSpan = TextSpan(
    text: test,
    style: TextStyle(
        fontSize: 14.r,
        fontWeight: FontWeight.w500));

final TextPainter textPainter =
    TextPainter(text: textSpan, textDirection: TextDirection.ltr);

// 使用 inputKey 获取 TextField 宽度
textPainter.layout(
    maxWidth:
        inputKey.currentContext!.size!.width);

// print(textPainter.size);
// print(textPainter.didExceedMaxLines);

List<LineMetrics> lines = textPainter.computeLineMetrics();

// 0 或 1 表示单行, >=1 表示多行
print(lines.length);
```

# Reference

* [Flutter 关于 TextField 你能知道的一切](https://juejin.cn/post/6844903889829888014)
* [【Flutter 专题】64 图解基本 TextField 文本输入框 (一)](https://xie.infoq.cn/article/a8c99a397a4c70634c0e4cf3e)