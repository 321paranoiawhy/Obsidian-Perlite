- [sse - pub.dev](https://pub.dev/packages/sse)
- [eventsource - pub.dev](https://pub.dev/packages/eventsource)
- [universal_html eventsource - pub.dev](https://pub.dev/packages/universal_html#eventsource)
- [EventSource class - dart:html](https://api.flutter.dev/flutter/dart-html/EventSource-class.html)
- [Server-sent_events - MDN](https://developer.mozilla.org/en-US/docs/Web/API/Server-sent_events)
- [flutter_sse - github](https://github.com/toshiossada/flutter_sse)
- [eventstore_client - pub.dev](https://pub.dev/packages/eventstore_client)
- [Server-Sent Events - gist](https://gist.github.com/sma/fa5ebd85fd54a2c973186d02c8fae467)
- [Server-sent-events - whatwg](https://html.spec.whatwg.org/multipage/server-sent-events.html)

## Dart 服务端

`yaml`:

```yaml
name: sse
description: A Example os shelf API using Server Sent Events
version: 1.0.0

environment:
  sdk: ">=2.16.1 <3.0.0"

dependencies:
  eventsource: ^0.4.0
  shelf: ^1.3.0
  shelf_router: ^1.1.2
  shelf_eventsource:
    git:
      url: https://github.com/toshiossada/dart-shelf_eventsource.git
      ref: master
dev_dependencies:
  lints: ^1.0.0
```

`main.dart`:

```dart
import "dart:async";
import 'dart:convert';

import 'package:eventsource/publisher.dart';
import "package:shelf/shelf_io.dart" as io;
import 'package:shelf_eventsource/shelf_eventsource.dart';
import 'package:shelf_router/shelf_router.dart';

main() {
  Router app = Router();

  app.get("/events", _handlerEventsWithoutUser);

  app.get("/events/<user>", _handlerEventsWithtUser);

  io.serve(app, "localhost", 8080);
  // io.serve(app, "10.10.21.86", 8080);
}

_handlerEventsWithoutUser(dynamic r) {
  final EventSourcePublisher publisher = EventSourcePublisher();
  generateEvents(publisher);
  var handler = eventSourceHandler(publisher);
  handler(r);
}

_handlerEventsWithtUser(dynamic request, String user) {
  final EventSourcePublisher publisher = EventSourcePublisher();
  generateEvents(publisher, user: user);
  var handler = eventSourceHandler(publisher, channel: user);
  handler(request);
}

generateEvents(
  EventSourcePublisher publisher, {
  String? user,
}) {
  int id = 0;
  Timer.periodic(const Duration(milliseconds: 500), (timer) {
    bool finished = id >= 5;

    final data = json.encode({
      'id': id,
      'message': 'event $id',
      'finished': finished,
      'user': user,
    });

    publisher.add(Event(data: data), channels: [user ?? '']);

    if (finished) {
      timer.cancel();

      publisher.close();
    }

    id++;
  });
}
```

运行:

```bash
dart run
```

输出:

```
Building package executable... 
Built sse:sse.
```

# curl 测试

`cmd`:

```bash
curl http://localhost:8080/events

curl -N http://localhost:8080/events
```

接口返回:

```
data: {"id":0,"message":"event 0","finished":false,"user":null}

data: {"id":1,"message":"event 1","finished":false,"user":null}

data: {"id":2,"message":"event 2","finished":false,"user":null}

data: {"id":3,"message":"event 3","finished":false,"user":null}

data: {"id":4,"message":"event 4","finished":false,"user":null}

data: {"id":5,"message":"event 5","finished":true,"user":null}
```

`PowerShell`:

```powershell
Invoke-RestMethod -Uri 'http://localhost:8080/events'
```

在 `PowerShell` 中 `curl` 是 `Invoke-WebRequest` 的别名, 其它别名为:

- `iwr`
- `wget`

可使用 `curl.exe` 替代 `curl`:

```powershell
curl.exe --help

curl.exe http://localhost:8080/events
```

Reference:

- [curl -N](https://stackoverflow.com/a/31255914)
- [Invoke-RestMethod -Uri](https://www.reddit.com/r/PowerShell/comments/g8p8ya/comment/foosszq/?utm_source=share&utm_medium=web2x&context=3)
- [Invoke-WebRequest - Powershell](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/invoke-webrequest?view=powershell-7.3)
- [Invoke-RestMethod - Powershell](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/invoke-restmethod?view=powershell-7.3)

# 浏览器测试

```js
const evtSource = new EventSource("http://localhost:8080/events", {
  withCredentials: true,
});

evtSource.onmessage = (event) => {
  console.log(event.data);
};
```

> [!error]
> Access to resource at 'http://localhost:8080/events' from origin 'null' has been blocked by CORS policy: The request client is not a secure context and the resource is in more-private address space `local`.

> [!tip]
> 浏览器上有 `CORS` 限制。

- [CSP: connect-src](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/connect-src)

# Node 测试

- [@microsoft/fetch-event-source](https://www.npmjs.com/package/@microsoft/fetch-event-source)