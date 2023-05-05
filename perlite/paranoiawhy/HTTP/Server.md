# Python SimpleHTTPServer

- [Python SimpleHTTPServer - Python HTTP Server](https://www.digitalocean.com/community/tutorials/python-simplehttpserver-http-server)

默认端口为 `8000`

`python 3` 以前:

```python
python -m SimpleHTTPServer 9000
```

> [!error]
> 如果在 `python 3` 以后运行上述命令会报错如下:
> No module named SimpleHTTPServer

`python 3`:

```bash
python -m http.server 9000
```

# Node http-server

[http-server](https://www.npmjs.com/package/http-server)

默认端口为 `8080`

```bash
npm install http-server -g
```

```bash
http-server -c-1 -p 9000
```

# Dart dhttpd

[dhttpd](https://pub.flutter-io.cn/packages/dhttpd)

默认端口为 `8080`

```bash
dhttpd --path build/web/
```

# Rust miniserver

[miniserver](https://github.com/svenstaro/miniserve)

默认端口为 `8080`