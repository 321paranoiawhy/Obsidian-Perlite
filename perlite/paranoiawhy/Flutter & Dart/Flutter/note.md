
# `!.`

```dart
Map testMap = {"A": "a", "B": "b", "C": "c"};
testMap!
```

# 定义可空变量 `null`

```dart
int intA = 1;
// 报错
intA = null;
// A value of type 'Null' can't be assigned to a variable of type 'int'.
// Try changing the type of the variable, 
// or casting the right-hand type to 'int'.
// dart[invalid_assignment](https://dart.dev/diagnostics/invalid_assignment)

// 正常运行
int? intB = 2;
intB = null;
```

# `operators`

[Operators - dart.dev](https://dart.dev/guides/language/language-tour#operators)

# Null Safety

> [!tip]
> 空安全在 Dart 2.12 版本之后引入。

- [Dart 2.x and null safety](https://dart.dev/null-safety#enable-null-safety)

In Dart 2.12 to 2.19, null safety is a configuration option in the pubspec. Null safety is not available in SDK versions prior to Dart 2.12.

To enable sound null safety, set the [SDK constraint lower-bound](https://dart.dev/tools/pub/pubspec#sdk-constraints) to a [language version](https://dart.dev/guides/language/evolution#language-versioning) of 2.12 or later. For example, your `pubspec.yaml` file might have the following constraints:

```yaml
environment:
  sdk: '>=2.12.0 <3.0.0'
```

# 冒泡背景

[Flutter 实现冒泡背景](https://wenjie.store/archives/flutter%E5%AE%9E%E7%8E%B0%E5%86%92%E6%B3%A1%E8%83%8C%E6%99%AF)

# `Google Assistant`

[Define capabilities in shortcuts.xml](https://developer.android.com/develop/ui/views/launch/shortcuts/adding-capabilities)

## `android:targetPackage`

> 跳转的目标应用包名

**android\app\src\main\AndroidManifest.xml**:

```xml
<!-- package 的值即为 android:targetPackage 的值 -->
<!-- net.touchcapture.qr.flutterqrexample -->
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="net.touchcapture.qr.flutterqrexample">
```

**android\app\src\main\res\xml\shortcuts.xml**:

```xml
android:targetPackage="net.touchcapture.qr.flutterqrexample"
```

## `android:targetClass`

> 跳转的目标类

**android\app\src\main\AndroidManifest.xml**:

```xml
<!-- android\app\src\main\AndroidManifest.xml -->
<!-- package + android:name 的值即为 android:targetClass 的值 -->
<!-- net.touchcapture.qr.flutterqrexample.io.flutter.embedding.android.FlutterActivity -->
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="net.touchcapture.qr.flutterqrexample">

<activity
	 android:name="io.flutter.embedding.android.FlutterActivity">
```

> [!hint]
> `AndroidManifest.xml`:
> 
> * [manifest](https://developer.android.com/guide/topics/manifest/manifest-element)
> * [manifest package](https://developer.android.com/guide/topics/manifest/manifest-element#package)
> * [activity](https://developer.android.com/guide/topics/manifest/activity-element)
> * [activity android:name](https://developer.android.com/guide/topics/manifest/activity-element#nm)

**android\app\src\main\res\xml\shortcuts.xml**:

```xml
<!-- android\app\src\main\res\xml\shortcuts.xml -->
android:targetClass="net.touchcapture.qr.flutterqrexample"
```

> [!info]
> 参考链接:
> 
> * [shortcuts.xml](https://android.googlesource.com/platform/packages/apps/Settings/+/master/res/xml/shortcuts.xml)

## `android:shortcutShortLabel`

> 快捷方式短标签 (简要描述)

[String resources](https://developer.android.com/guide/topics/resources/string-resource)

**android\app\src\main\res\values\strings.xml** 配置字符串资源:

```xml
<!-- android\app\src\main\res\values\strings.xml -->
<?xml version="1.0" encoding="utf-8"?>

<resources>
    <string
        name="example"
        >example_string</string>
</resources>
```

**android\app\src\main\res\xml\shortcuts.xml**:

```xml
<!-- android\app\src\main\res\xml\shortcuts.xml -->
<shortcut android:shortcutShortLabel="@string/example"></shortcut>
```

> [!hint]
> [Customize attribute values](https://developer.android.com/develop/ui/views/launch/shortcuts/creating-shortcuts#static)
> 
> 每个 `shortcut` 标签中必须配置有 `android:shortcutId` 和`android:shortcutShortLabel` 属性。
> 
> 其中 `android:shortcutId` 属性值不能为字符串资源, `android:shortcutShortLabel` 属性值只能为字符串资源 (`@string/example`) 且可能的话长度不超过 `10`。
> 
> `android:enabled` 值为 `true` 或 `false`, 表示是否启用快捷方式。
> 
> `android:icon` 为快捷方式的图标配置。

## `android:shortcutLongLabel`

> 快捷方式长标签 (详细描述)

> [!hint]
> `android:shortcutLongLabel` 可能的话长度不超过 `25`。

## `intent`

> [!hint]
> `intent` 标签必须有 `android:action` 属性, 其默认值为 `android.intent.action.VIEW`。
> 
> 当用户通过语音或触摸启动此快捷方式时，系统就会执行此 `intent`。

> [!hint]
> 所有 `intent` 可选值列表:
> 
> [intent Constants](https://developer.android.com/reference/android/content/Intent#constants_1)
> 
> * [ACTION_MAIN](https://developer.android.com/reference/android/content/Intent#ACTION_MAIN) 作为主入口点启动
> * [ACTION_VIEW](https://developer.android.com/reference/android/content/Intent#ACTION_VIEW) 查看数据
> * [ACTION_RUN](https://developer.android.com/reference/android/content/Intent#ACTION_RUN) 运行应用
> * [ACTION_SEARCH](https://developer.android.com/reference/android/content/Intent#ACTION_SEARCH)
> * [ACTION_WEB_SEARCH](https://developer.android.com/reference/android/content/Intent#ACTION_WEB_SEARCH)
> * [ACTION_WIFI_SETTINGS](https://developer.android.com/reference/android/provider/Settings#ACTION_WIFI_SETTINGS) `android.settings.WIFI_SETTINGS`
> * [ACTION_POWER_USAGE_SUMMARY](https://developer.android.com/reference/android/content/Intent#ACTION_POWER_USAGE_SUMMARY)

```
## `capability-binding`

[capability-binding](https://developer.android.com/guide/app-actions/action-schema#capability-binding)

```xml
<capability-binding android:key="actions.intent.SCAN" />
```

> [!hint]
> `android:key` 属性值同 `capability` 的 `android:name` 属性值。