- [Flutter 的单例模式 - Dart 化](https://flutter.cn/community/tutorials/singleton-pattern-in-flutter-n-dart#dart-%E5%8C%96)

```dart
class Singleton {
  Singleton._internal();
  
  factory Singleton() => _instance;
  
  static late final Singleton _instance = Singleton._internal();
}
```

# 使用 get_it 插件

- [get_it](https://pub.dev/packages/get_it)