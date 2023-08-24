## 视频播放器

- [flutter_vlc_player](https://pub.dev/packages/flutter_vlc_player) vlc_player
- [video_player](https://pub.dev/packages/video_player) 官方出品的 video_player
- [better_player](https://pub.dev/packages/better_player)
- [fijkplayer](https://pub.dev/packages/fijkplayer) `Bilibili` ijkplayer 移植版
- [chewie](https://pub.dev/packages/chewie) 基于 `video_player`
- [dart_vlc](https://pub.dev/packages/dart_vlc) 仅支持 `Windows` 和 `Linux`
- [media_kit](https://pub.dev/packages/media_kit) 基于 `libmpv`, 底层为 [mpv-player](https://mpv.io/)

`windows` 下命令行打开 `rtsp` 链接:

```bash
# https://github.com/mpv-player/mpv/issues/4845#issuecomment-1151929780
mpv rtsp://10.10.21.201:8083/test --rtsp-transport=udp
```

## 图片

- [cached_network_image](https://pub.dev/packages/cached_network_image) 网络图片缓存
- [flutter_svg](https://pub.dev/packages/flutter_svg) SVG 图片格式支持

## 动画

- [lottie](https://pub.dev/packages/lottie) `Airbnb` Lottie 动画库

## Toast & Dialog

- [fluttertoast](https://pub.dev/packages/fluttertoast)
- [flutter_smart_dialog](https://pub.dev/packages/flutter_smart_dialog)
- [flutter_easyloading](https://pub.dev/packages/flutter_easyloading)
- [oktoast](https://pub.dev/packages/oktoast)

```dart
ScaffoldMessenger.of(context).showSnackBar(
	SnackBar(content: Text('snack bar'))
);
```

## 存储

- [shared_preferences](https://pub.dev/packages/shared_preferences) 本地存储

## 图标

- [flutter_launcher_icons](https://pub.dev/packages/flutter_launcher_icons) APP 图标生成工具
- [icons_launcher](https://pub.dev/packages/icons_launcher)

## 界面

- [flutter_app_badger](https://pub.dev/packages/flutter_app_badger) 桌面图标右上角显示消息数量

## Markdown

- [flutter_markdown](https://pub.dev/packages/flutter_markdown) 渲染 `Markdown` 组件
- [markdown_editable_textinput](https://pub.dev/packages/markdown_editable_textinput) 可编辑 `Markdown` 输入框
- [markdown](https://pub.dev/packages/markdown) 在客户端和服务端将 `Markdown` 转换为 `HTML`

在线预览:

- [markdownlivepreview](https://markdownlivepreview.com/)
- [Dart Markdown Live Editor](https://dart-lang.github.io/markdown/)

# Webview

- [webview_flutter](https://pub.dev/packages/webview_flutter)
- [flutter_inappwebview](https://pub.dev/packages/flutter_inappwebview)
- [flutter_webview_plugin](https://pub.dev/packages/flutter_webview_plugin) 已停止维护