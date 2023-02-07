#Lifecycle #StatelessWidget #StatefulWidget #AppLifecycleState
# `StatelessWidget`

## `build`

# `StatefulWidget`

# `AppLifecycleState`

```dart
@override
void didChangeAppLifecycleState(AppLifecycleState state) {
  super.didChangeAppLifecycleState(state);
  print(state);
  if (state == AppLifecycleState.paused) {
    // went to Background
  }
  if (state == AppLifecycleState.resumed) {
    // came back to Foreground
  }
}
```

> [!note]
> `AppLifecycleState` 枚举值如下:
> - paused: `APP` 退出至后台
> - resumed: `APP` 重新显示
> - inactive
> - detached

- [AppLifecycleState enum](https://api.flutter.dev/flutter/dart-ui/AppLifecycleState.html)