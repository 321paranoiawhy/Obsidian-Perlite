- [Flutter 的单例模式 - Dart 化](https://flutter.cn/community/tutorials/singleton-pattern-in-flutter-n-dart#dart-%E5%8C%96)

```dart
class Singleton {
  Singleton._internal();
  
  factory Singleton() => _instance;
  
  static late final Singleton _instance = Singleton._internal();
}
```
