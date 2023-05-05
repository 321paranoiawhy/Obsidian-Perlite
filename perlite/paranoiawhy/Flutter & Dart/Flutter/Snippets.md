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

- []()
- [将 WebView 添加到您的 Flutter 应用](https://codelabs.developers.google.com/codelabs/flutter-webview?hl=zh-cn#0)