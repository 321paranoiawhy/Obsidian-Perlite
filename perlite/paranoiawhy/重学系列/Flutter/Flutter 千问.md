# 滚动组件滚动到顶部/底部

```dart
// 滚动到顶部
Future<void> _scrollListToEnd() async {
  await Future.delayed(const Duration(milliseconds: 500));
  
  _controller.animateTo(_controller.position.minScrollExtent,
      duration: const Duration(milliseconds: 200), curve: Curves.easeInOut);
}

// 滚动到底部
Future<void> _scrollListToEnd() async {
  await Future.delayed(const Duration(milliseconds: 500));
  
  _controller.animateTo(_controller.position.maxScrollExtent,
      duration: const Duration(milliseconds: 200), curve: Curves.easeInOut);
}
```

注意在上述代码中在使用控制器滚动前须延时**一定时间**(可为一帧, 或 `200ms`、`300ms`、`500ms` 等), 否则 `Widget` 尚未渲染出来, 滚动到顶部/底部不生效。

在 `Flutter` 中可滚动组件有:

- `ListView`
- `GridView`
- `SingleChildScrollView`
- `CustomScrollView`

滚动到指定下标 `Widget` 可使用以下插件:

- [scrollable_positioned_list](https://pub.dev/packages/scrollable_positioned_list)
- [scroll_to_index](https://pub.dev/packages/scroll_to_index)
- [scrollview_observer](https://pub.dev/packages/scrollview_observer)
- [indexed_list_view](https://pub.dev/packages/indexed_list_view)

# 单行文本过长显示省略号

```dart
Text(
	'这是一段很长很长很长很长很长很长很长很长很长很长的文本'
	overflow: TextOverflow.ellipsis,
)
```

注意 `Text` 需要限定宽度, 或者在 `Row/Column` 组件内使用 `Expanded` 包裹 `Text`, 否则溢出效果不生效。

# Text 自动换行

添加 `softWrap: true` 即可:

```dart
Text(
	'这是一段很长很长很长很长很长很长很长很长很长很长的文本'
	softWrap: true,
)
```

# 字符串重复多次

```dart
// 等价于 '字符串字符串字符串字符串字符串'
'字符串' * 5
```

# 浅复制和深复制

## 浅复制

`List` 浅复制:

```dart
List<int> list = [1, 2, 3];

var list1 = list.toList();
var list2 = [...list];
var list3 = List.from(list); // type: List<dynamic>
var list4 = List.of(list); // type: List<int>
var list5 = List.unmodifiable(list); // 不可变(长度)
var list6 = []..addAll(list);
```

## 深复制

```dart
jsonDecode(jsonEncode(data));

json.decode(json.encode(data));
```

# 使用尚未发布的插件

如果一个插件未发布到 `pub.dev`, 但可以获取其 `git` 仓库地址, 则可在 `pubspec.yaml` 中按如下设定:

```yaml
dependencies:
  unpublished_plugin:
    git:
      url: <git repo url>
      ref: <The branch, tag, or anything else Git allows to identify a commit.>
```

`ref` 可选值为:

- `branch`, 如 `master`、 `dev` 等
- `tag`, 如 `release`、 `alpha`、 `pre-release`

# 运行时添加参数

命令行:

```bash
flutter run --debug
flutter run --profile
flutter run --release
```

打包 `android`:

```bash
flutter build apk

flutter build apk --split-per-abi --verbose
```

打包 `iOS`:

```bash
flutter build ipa
```

## `VS Code` 配置 `launch.json`

配置 `configurations` 各项的 `args`:

```json
{
    // Use IntelliSense to learn about possible attributes.
    // Hover to view descriptions of existing attributes.
    // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
        {
            "name": "frontend-example-app",
            "request": "launch",
            "type": "dart",
            // "flutterMode": "debug",
            "args": [
                "--no-sound-null-safety"
            ]
        },
        {
            "name": "frontend-example-app (profile mode)",
            "request": "launch",
            "type": "dart",
            "flutterMode": "profile"
        },
        {
            "name": "frontend-example-app (release mode)",
            "request": "launch",
            "type": "dart",
            "flutterMode": "release"
        }
    ]
}
```

`--no-sound-null-safety` 表示禁用空安全特性, [详情](https://dart.dev/null-safety/unsound-null-safety#testing-or-running-mixed-version-programs)

设定 `web` 端口号:

```bash
flutter run -d chrome --web-port=1234
```

# `flutter_screenutil`

`verticalSpace` 和 `horizontalSpace`: 

```dart
16.verticalSpace

16.horizontalSpace
```

# iOS 相关

## TMS-90078: Missing Push Notification Entitlement

- [Flutter/App Store Connect Warning: ITMS-90078 Missing Push Notification Entitlement](https://www.ernestchiang.com/en/posts/2020/flutter-itms-90078-missing-push-notification-entitlement/)

1. Open the Flutter project (Runner) in XCode.
2. Enable "Push Notifications" under Capabilities. (refer to the screenshot below)
3. XCode will generate the “ios/Runner/Runner.entitlements” file.
4. Done.

`XCode` 会生成 `ios/Runner/Runner.entitlements` 文件:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
	<key>aps-environment</key>
	<string>development</string>
</dict>
</plist>
```

# 去除右上角 debug 文本

设置 `MaterialApp.debugShowCheckedModeBanner` 属性值为 `false`:

```dart
MaterialApp(
	debugShowCheckedModeBanner: false,
);
```

全局配置:

# TextField 自适应高度

## minLines 和 maxLines

最少显示 `minLines` 行, 最多显示 `maxLines` 行:

```dart
TextField(
	minLines: 1,
	maxLines: 10,
)
```

## InputDecoration.constraints

```dart
TextField(
	decoration: InputDecoration(
		constraints: BoxConstraints(minHeight: 50, maxHeight: 200),
	),
)
```

# IIFE 立即执行函数

```dart
(){
	print('IIFE');
}();
```

# 获取图片原始尺寸

```dart
import 'dart:ui' as ui;
import 'dart:async';
import 'package:flutter/material.dart';

class GetImageInfo extends StatelessWidget {
  const GetImageInfo({Key? key}) : super(key: key);
  
  @override
  Widget build(BuildContext context) {
    Image image = Image.network('https://i.stack.imgur.com/lkd0a.png');
    Completer<ui.Image> completer = Completer<ui.Image>();
    image.image
        .resolve(const ImageConfiguration())
        .addListener(ImageStreamListener((ImageInfo info, bool _) {
      completer.complete(info.image);
      print("image info: $info");
    }));
    return const Placeholder();
  }
}
```

- [how-do-i-determine-the-width-and-height-of-an-image-in-flutter - stackoverflow](https://stackoverflow.com/questions/44665955/how-do-i-determine-the-width-and-height-of-an-image-in-flutter)

# 可选链

`...?`

```dart
final List? list = null;

// 如果 list 为 null, newList 则为空数组
// 否则, newList 为 list 的浅复制
final newList = [...?list];
```

`?.`:

```dart
context.size?.width;
```

`?[]`:

```dart
final List? list = null;

print(list?[0]);
```

# 在 build 方法里条件

`if...else`:

```dart
if(true)
	SizedBox(width: 10, height: 10)
else
	SizedBox(width: 20, height: 20)
```

三元运算符:

```dart
true ? SizedBox(width: 10, height: 10)
```

# VS Code

### 设置自动保存并格式化

- [Is there a way to auto-format flutter with vscode?](https://stackoverflow.com/a/67472237)

`.vscode/settings.json`:

```json
{
  // 保存自动格式化代码
  "editor.formatOnSave": true,
  // 配置 Tab 空格数
  "editor.tabSize": 2,
  "[dart]": {
    "editor.defaultFormatter": "Dart-Code.dart-code",
    "editor.formatOnSave": true
  }
}
```
