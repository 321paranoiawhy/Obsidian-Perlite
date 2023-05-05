# `server.host`

[server-host](https://cn.vitejs.dev/config/server-options.html#server-host)

`vite.config.ts`:

```
// vite.config.ts
import { defineConfig } from 'vite'
import vue from '@vitejs/plugin-vue'

// https://vitejs.dev/config/
export default defineConfig({
  plugins: [vue()],
  server: {
    host: "0.0.0.0", // server.host: https://cn.vitejs.dev/config/server-options.html#server-host
  }
})
```

```bash
npm run dev --host
```

> [!info]
> VITE v4.0.3  ready in 288 ms
> 
>   ➜  Local:   http://localhost:5173/
>   ➜  Network: http://10.10.21.86:5173/
>   ➜  press h to show help

# 生产环境下去除 console 和 debug

- [vite 项目当中移除项 console](https://zhuanlan.zhihu.com/p/610491428)

## build.minify 为 esbuild

- [build.minify - Vite](https://vitejs.dev/config/build-options.html#build-minify)
- [Conditional Config - Vite](https://vitejs.dev/config/#conditional-config)
- [Modes - Vite](https://vitejs.dev/guide/env-and-mode.html#modes)

`build.minify` 默认值 `esbuild`:

```ts
export default defineConfig(({ mode }) => ({
  esbuild: {
    drop: mode === 'production' ? ['console', 'debugger'] : []
  },
  build: {
    minify: 'esbuild'
  }
}))
```

## build.minify 为 terser

- [build.terserOptions - Vite](https://vitejs.dev/config/build-options.html#build-terseroptions)
- [Compress options - terser](https://terser.org/docs/api-reference#compress-options)

```ts
export default defineConfig({
  build: {
    minify: 'terser',
    terserOptions: {
      compress: {
        drop_console: true,
        drop_debugger: true // default true
      }
    }
  },
})
```

# vite-plugin-compression

- [vite-plugin-compression - npm](https://www.npmjs.com/package/vite-plugin-compression)
 - [vite-plugin-compression - GitHub](https://github.com/vbenjs/vite-plugin-compression)

下载:

```bash
# npm
npm i vite-plugin-compression -D

# yarn
yarn add vite-plugin-compression -D
```

`vite.config.ts`:

```ts
import viteCompression from 'vite-plugin-compression';

export default defineConfig({
  plugins: [vue(), viteCompression()],
})
```

> [!tip]
> `npm run build` 后把 `dist` 文件夹上传到服务器并开启 `GZip` 即可。

# vue-router history 和 hash

`history` 模式对于单页面应用 (`SPA, Single Page Application`) 在浏览器中直接输入某个页面的链接会出现 `404` 的情况, 此时须在服务器做相应配置, 如 `nginx` 配置:

```nginx
server
    {
        listen 80; // 服务端口号
        server_name phpmyadmin;
        index index.html index.htm index.php;
        location /neimenmenhuan {
        proxy_pass http://localhost:8080;  // 配置后端接口端口
      }
      location / {
        root  /www/server/phpmyadmin;   // 根目录位置
        index index.html index.htm index.php;  / /默认入口文件
        try_files $uri $uri /index.html;  // 出错重定向 index.html 问题解决于此  
      }
    

      access_log  /www/wwwlogs/access.log;
    }
```
