#CORS #JSONP
# `JSONP`

# `Fetch JSONP`

- [Fetch JSONP](https://github.com/camsong/fetch-jsonp)

> [!important]
> 同 `JSONP` , `Fetch JSONP` 也只支持 `GET` 请求。

请求示例:

```js
const GistURL = "https://gist.github.com/5149b8848cb05f20efbc21fa750d7d2e.json";
 
const fetchGist = async (url: string) => {
	const response = await fetchJSONP(url);
	console.log("response", response, response.ok);
	if (response.ok) {
		const result: GistResponse = await response.json();
		console.log("result", result);
	} else {
	    console.log("error");
	}
};

fetchGist(GistURL);
```

```gist
5149b8848cb05f20efbc21fa750d7d2e
```