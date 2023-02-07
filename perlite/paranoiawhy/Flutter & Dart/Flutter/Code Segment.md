#Flutter #CodeSegment
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