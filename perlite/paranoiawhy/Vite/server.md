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