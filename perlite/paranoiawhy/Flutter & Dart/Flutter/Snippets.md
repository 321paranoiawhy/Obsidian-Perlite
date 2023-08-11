# 获取二进制图片数据并展示

## API 接口

```dart
import 'package:http/http.dart' as http;
import 'dart:typed_data'; // Uint8List type

// https://stackoverflow.com/questions/68666059/flutter-byte-array-response-body-to-file
// 返回 Uint8List
Future<Uint8List> fetchBinaryImage(String url) async {
  http.Response response = await http.get(Uri.parse(url));
  return response.bodyBytes;
}
```

## 展示

```dart
Widget buildImage() async {
  Uint8List response = await fetchBinaryImage(
      'https://upload.wikimedia.org/wikipedia/en/a/a9/Example.jpg');
  return Image.memory(response);
}
```

- [http Response bodyBytes property](https://pub.dev/documentation/http/latest/http/Response/bodyBytes.html)

# 下载图片到本地

```dart
import 'dart:io'; // File

import 'package:flutter/material.dart';
import 'package:flutter_file_dialog/flutter_file_dialog.dart';
import 'package:http/http.dart' as http;
import 'package:path_provider/path_provider.dart';

Future<void> _saveImage(BuildContext context, String url) async {
  String? message;
  final scaffoldMessenger = ScaffoldMessenger.of(context);

  try {
    // Download image
    final http.Response response = await http.get(Uri.parse(url));

    // Get temporary directory
    final dir = await getTemporaryDirectory();

    // Create an image name
    var filename = '${dir.path}/test/saved_iamge.png';

    // Save to filesystem
    final file = File(filename);
    await file.writeAsBytes(response.bodyBytes);

    // Ask the user to save it
    final params = SaveFileDialogParams(sourceFilePath: file.path);
    final finalPath = await FlutterFileDialog.saveFile(params: params);

    if (finalPath != null) {
      message = 'Image saved to disk.';
    }
  } catch (e) {
    message = 'An error occurred while saving the image.';
  }

  if (message != null) {
    scaffoldMessenger.showSnackBar(SnackBar(content: Text(message)));
  }
}
```

# 接入第三方平台登录

## Google

`api.dart`:

```dart
import 'dart:convert';
import 'package:http/http.dart' as http;

Future<http.Response> verifyIdToken(Map<String, String> body) async {
  Uri url = Uri.parse('https://dev-api.cereb.ai/v1/login/google_oauth2');
  http.Response response = await http.post(url, body: json.encode(body));
  return response;
}
```

`login.dart`:

```dart
import 'package:google_sign_in/google_sign_in.dart';
import '../api.dart' as api;

/// Google 账号登录
Future<void> onGoogleSignIn() async {
  final GoogleSignIn _googleSignIn = GoogleSignIn(
    // Optional clientId
    // https://medium.com/@druhin.bala/google-signin-without-firebase-for-android-on-flutter-e3ee834f696e
    clientId:
        '998005764794-ct09ghhrlaft05f1eau9i64f1ksf5noj.apps.googleusercontent.com',
    scopes: [
      'https://www.googleapis.com/auth/userinfo.email',
      'openid',
      'https://www.googleapis.com/auth/userinfo.profile',
    ],
  );
  
  try {
    // GoogleSignInAccount 下面有以下属性: displayName / email / id / photoUrl / serverAuthCode
    // https://pub.dev/documentation/google_sign_in/latest/google_sign_in/GoogleSignInAccount-class.html
    final GoogleSignInAccount? googleUser = await _googleSignIn.signIn();

    // GoogleSignInAuthentication 下面有以下属性: accessToken / idToken
    // https://pub.dev/documentation/google_sign_in/latest/google_sign_in/GoogleSignInAuthentication-class.html
    final GoogleSignInAuthentication? googleAuth =
        await googleUser?.authentication;

    if (googleAuth?.idToken != null) {
      var res = await api.verifyIdToken({'id_token': googleAuth?.idToken});
      debugPrint('res: $res');
    } else {
      debugPrint('idToken is null.');
    }
  } catch (error) {
    debugPrint('error: $error');
  }
}
```

`python` 校验 `idToken`:

```python
# https://google-auth.readthedocs.io/en/stable/reference/google.oauth2.id_token.html
from google.oauth2 import id_token
from google.auth.transport import requests
from aiohttp import web

GOOGLE_CLIENT_ID: str = '998005764794-ct09ghhrlaft05f1eau9i64f1ksf5noj.apps.googleusercontent.com'

# https://developers.google.com/identity/gsi/web/guides/verify-google-id-token?hl=zh-cn#using-a-google-api-client-library
def verify_id_token(token:str):
    try:
        id_info = id_token.verify_oauth2_token(token, requests.Request(),
                                               GOOGLE_CLIENT_ID)
        print(id_info)
        if id_info['iss'] not in [
                'accounts.google.com', 'https://accounts.google.com'
        ]:
            return (False, "Could not verify token signature.")
        return ((True, "Token verified"))
    except ValueError as e:
        print(e)  #o r Log the error
        return (False, "Could not verify token signature.")


routes = web.RouteTableDef()


@routes.post('/verify_id_token')
async def store_mp3_handler(request):
    data = await request.json()
    # print(data)
    user_id_token:str = data['id_token']
    print(len(data['id_token']))
    print(verify_id_token(user_id_token))

    # https://developers.google.com/identity/sign-in/web/backend-auth?hl=zh-cn#calling-the-tokeninfo-endpoint
    return web.Response(text="OK")


app = web.Application()
app.add_routes(routes)
web.run_app(app, port=1234)
```

# 一些常量

- [kDebugMode top-level constant](https://api.flutter.dev/flutter/foundation/kDebugMode-constant.html)
- [kReleaseMode top-level constant](https://api.flutter.dev/flutter/foundation/kReleaseMode-constant.html)
- [kProfileMode top-level constant](https://api.flutter.dev/flutter/foundation/kProfileMode-constant.html)
- [Platform class](https://api.flutter.dev/flutter/package-platform_platform/Platform-class.html)
- [kIsWeb top-level constant](https://api.flutter.dev/flutter/foundation/kIsWeb-constant.html)

- `kXMode`:
	- `kDebugMode`
	- `kReleaseMode`
	- `kProfileMode`
- `Platform.isX`:
	- `Platform.isAndroid`
	- `Platform.isFuchsia`
	- `Platform.isIOS`
	- `Platform.isLinux`
	- `Platform.isMacOS`
	- `Platform.isWindows`
- `kIsWeb`

```dart
import 'dart:io' show Platform;

print('isAndroid: ${Platform.isAndroid}');
```

```dart
import 'package:flutter/foundation.dart'

print('kDebugMode: $kDebugMode');

print('kIsWeb: $kIsWeb');
```

# 按钮

- [按钮 - Flutter 实战·第二版](https://book.flutterchina.club/chapter3/buttons.html#_3-2-1-elevatedbutton)

## 圆形按钮

设置 `Container.decoration.shape` 为 `BoxShape.circle`:

```dart
Container(
	decoration: BoxDecoration(
		shape: BoxShape.circle,
	),
)
```

`CircleAvatar`:

```dart
CircleAvatar(
  // 头像半径
  radius: 60,
  // 头像图片
  backgroundImage: Image.asset('example.png'),
)
```

`ClipOval`:

```dart
ClipOval(
  child: Image.asset('example.png'),
)
```

`ClipRRect`:

```dart
ClipRRect(
  borderRadius: BorderRadius.circular(30),
  child: Image.asset('example.png', width: 60, height: 60, fit: BoxFit.cover),
)
```

## 各种边框形状

- 斜切角: `BeveledRectangleBorder`
- 圆角: `RoundedRectangleBorder`
- 超椭圆: `SuperellipseShape`
- 体育场: `StadiumBorder`
- 圆形: `CircleBorder`

# 更改图片颜色

- [Color Filtered Widget — Apply multiple colors over images in Flutter | Image Color Filters](https://medium.com/vijay-r/color-filtered-widget-apply-multiple-colors-over-images-in-flutter-image-color-filters-746f45f90080)
- [ColorFiltered class](https://api.flutter.dev/flutter/widgets/ColorFiltered-class.html)

查看 `BlendMode` 所有枚举值:

```dart
BlendMode.values
```

> [!info] BlendMode.values
> [BlendMode.clear, BlendMode.src, BlendMode.dst, BlendMode.srcOver, BlendMode.dstOver, BlendMode.srcIn, BlendMode.dstIn, BlendMode.srcOut, BlendMode.dstOut, BlendMode.srcATop, BlendMode.dstATop, BlendMode.xor, BlendMode.plus, BlendMode.modulate, BlendMode.screen, BlendMode.overlay, BlendMode.darken, BlendMode.lighten, BlendMode.colorDodge, BlendMode.colorBurn, BlendMode.hardLight, BlendMode.softLight, BlendMode.difference, BlendMode.exclusion, BlendMode.multiply, BlendMode.hue, BlendMode.saturation, BlendMode.color, BlendMode.luminosity]

# 保持列表滚动位置

## AutomaticKeepAliveClientMixin

- [AutomaticKeepAliveClientMixin](https://api.flutter.dev/flutter/widgets/AutomaticKeepAliveClientMixin-mixin.html)
- [AutomaticKeepAlive详解](https://juejin.cn/post/6979972557575782407)

```dart
// 混入 `AutomaticKeepAliveClientMixin`
class _KeepAliveState extends State<MyListItem>
    with AutomaticKeepAliveClientMixin {
  @override
  Widget build(BuildContext context) {
    return Placeholder();
  }

  @override
  // 覆写 `wantKeepAlive` 返回 `true`
  bool get wantKeepAlive => true;
}
```

## PageStorageKey

- [PageStorageKey](https://api.flutter.dev/flutter/widgets/PageStorageKey-class.html)
- [滚动位置恢复](https://book.flutterchina.club/chapter6/scroll_controller.html#_3-滚动位置恢复)

```dart
SingleChildScrollView(key: const PageStorageKey(1))
```

# WebView

- [将 WebView 添加到您的 Flutter 应用](https://codelabs.developers.google.com/codelabs/flutter-webview?hl=zh-cn#0)

## Flutter webview 加载本地 HTML 文件

- [加载本地文件](https://juejin.cn/post/7032940950468952078#heading-3)
- [Flutter 开发：项目加载本地 html 文件的步骤](https://xie.infoq.cn/article/b96fe89b678d38ce1d04442eb)

在 `pubsec.yaml` 中声明 `index.html` 文件的路径:

```yaml
flutter:
	assets:
		- assets/index.html
```

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

# 去除滚动容器的水波纹效果

`Flutter` 滚动容器在安卓等平台上滚动到顶部和底部都会出现水波纹, 有些时候是不想要这个效果的, 可通过以下两种方式予以去除:

- `ScrollConfiguration`
- `NotificationListener`

### ScrollConfiguration

```dart
/// 自定义一个 NoShadowScrollBehavior
///
/// 去除 Android 的水波纹效果
class NoGlowScrollBehavior extends ScrollBehavior {
  @override
  Widget buildViewportChrome(
      BuildContext context, Widget child, AxisDirection axisDirection) {
    switch (getPlatform(context)) {
      case TargetPlatform.iOS:
      case TargetPlatform.macOS:
        return child;
      case TargetPlatform.android:
      case TargetPlatform.fuchsia:
      case TargetPlatform.linux:
      case TargetPlatform.windows:
        return GlowingOverscrollIndicator(
          child: child,
          // 不显示头部水波纹
          showLeading: false,
          // 不显示尾部水波纹
          showTrailing: false,
          axisDirection: axisDirection,
          // https://docs.flutter.dev/release/breaking-changes/theme-data-accent-properties#accentcolor
          // color: Theme.of(context).accentColor,
          color: Theme.of(context).colorScheme.secondary,
        );
    }
  }
}
```

可简写为:

```dart
class NoGlowScrollBehavior extends ScrollBehavior {
  const NoGlowScrollBehavior();

  @override
  Widget buildViewportChrome(
    BuildContext context,
    Widget child,
    AxisDirection axisDirection,
  ) =>
      child;
}
```

按如下方式**局部调用**:

```dart
ScrollConfiguration(
    behavior: NoGlowScrollBehavior(),
    child: SingleChildScrollView(
      child: ...
    )
);
```

> [!tip]
> 滚动容器有:
> 
> - `SingleChildScrollView`
> - `ListView`
> - `GridView`
> - `PageView`
> - `SingleChildScrollView`
> - `TabBarView`
> - `AnimatedList`

全局调用:

```dart
MaterialApp(
  builder: (BuildContext _, Widget? child) => ScrollConfiguration(
    behavior: const NoGlowScrollBehavior(),
    child: child!,
  ),
);
```

### NotificationListener

使用 `NotificationListener`:

```dart
NotificationListener<OverscrollIndicatorNotification>(
    onNotification: (OverscrollIndicatorNotification? overscroll) {
      // overscroll?.disallowGlow();
      overscroll?.disallowIndicator();
      return true;
    },
  child: ...,
),
```

# 去除按钮的水波纹效果

- [Flutter 彻底去除水波纹效果](https://blog.csdn.net/studying_ios/article/details/107342953)
- [Flutter 禁用水波纹](https://blog.bombox.org/2020-06-12/flutter-disable-ripple/)

```dart
class NoSplashFactory extends InteractiveInkFeatureFactory {
  @override
  InteractiveInkFeature create({
    required MaterialInkController controller,
    required RenderBox referenceBox,
    required Offset position,
    required Color color,
    required TextDirection textDirection,
    bool containedInkWell = false,
    RectCallback? rectCallback,
    BorderRadius? borderRadius,
    ShapeBorder? customBorder,
    double? radius,
    VoidCallback? onRemoved,
  }) {
    return _NoInteractiveInkFeature(
        controller: controller, referenceBox: referenceBox, color: color);
  }
}

class _NoInteractiveInkFeature extends InteractiveInkFeature {
  _NoInteractiveInkFeature({
    required MaterialInkController controller,
    required RenderBox referenceBox,
    required Color color,
    VoidCallback? onRemoved,
  }) : super(
            controller: controller,
            referenceBox: referenceBox,
            color: color,
            onRemoved: onRemoved);

  @override
  void paintFeature(Canvas canvas, Matrix4 transform) {}
}
```

`ThemeData` 中**全局**或**局部**配置:

```dart
ThemeData(
	splashFactory: NoSplashFactory(),
	// 按钮点击时的高亮颜色
	highlightColor: Colors.transparent,
	// 按钮点击后不松手的水波纹扩散颜色
	splashColor: Colors.transparent,
)
```

带水波纹效果的组件:

- `RaisedButton`
- `InkWell`
- `BottomNavigationBarItem`
