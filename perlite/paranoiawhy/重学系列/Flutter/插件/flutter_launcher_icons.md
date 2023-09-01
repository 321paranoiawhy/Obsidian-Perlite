- [flutter_launcher_icons - pub.dev](https://pub.dev/packages/flutter_launcher_icons)

`pubspec.yaml` 配置:

```yaml
flutter_launcher_icons:
  android: "launcher_icon"
  ios: true
  image_path: "images/app-logo.png"
  web:
    generate: true
    image_path: "path/to/app-logo.png"
    background_color: "#hexcode"
    theme_color: "#hexcode"
  windows:
    generate: true
    image_path: "path/to/app-logo.png"
    icon_size: 48 # min:48, max:256, default: 48
  macos:
    generate: true
    image_path: "path/to/app-logo.png"
```

生成图标:

```bash
flutter pub run flutter_launcher_icons:main

fvm flutter pub run flutter_launcher_icons:main
```