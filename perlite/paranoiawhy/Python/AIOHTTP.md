#Python #AIOHTTP

- [AIPHTTP Docs](https://docs.aiohttp.org/en/stable/)
- [aiohttp GitHub](https://github.com/aio-libs/aiohttp)

# `Client Example`

- [aiohttp Client API](https://docs.aiohttp.org/en/stable/client.html#aiohttp-client)

```python
import aiohttp
import asyncio

async def main():

    async with aiohttp.ClientSession() as session:
        async with session.get('http://python.org') as response:

            print("Status:", response.status)
            print("Content-type:", response.headers['content-type'])

            html = await response.text()
            print("Body:", html[:15], "...")

loop = asyncio.get_event_loop()
loop.run_until_complete(main())
```

> [!danger] DeprecationWarning
> DeprecationWarning: There is no current event loop
>   loop = asyncio.get_event_loop()

[参考 stackoverflow](https://stackoverflow.com/questions/73361664/asyncio-get-event-loop-deprecationwarning-there-is-no-current-event-loop),将 `loop = asyncio.get_event_loop()` 改为 `loop = asyncio.new_event_loop()` 即可。

# `Server Example`

- [aiohttp Server API](https://docs.aiohttp.org/en/stable/web.html#aiohttp-web)

```python
from aiohttp import web

async def handle(request):
    name = request.match_info.get('name', "Anonymous")
    text = "Hello, " + name
    return web.Response(text=text)

app = web.Application()
app.add_routes([web.get('/', handle),
                web.get('/{name}', handle)])

if __name__ == '__main__':
    web.run_app(app)
```

# `Middlewares`

- [aiohttp Middlewares](https://docs.aiohttp.org/en/stable/web_advanced.html#aiohttp-web-middlewares)