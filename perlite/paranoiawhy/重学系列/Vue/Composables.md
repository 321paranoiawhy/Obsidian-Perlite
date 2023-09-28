# useRouter 等 composables 只能在 setup 生命周期中使用

在 `axios` 拦截器中如果这样使用会获取不到 `router` 实例:

```ts
// axios 拦截器中, 不在 setup 中
const { router } = useRouter();

console.log(router); // undefined
```

可以直接导入 `router`:

```ts
import router from './router';

console.log(router); // 不为 undefined
```

接口 `401` 后跳转登录页实现方式:

1. 直接在 `axios` 响应拦截器里做跳转, 需要在此引入 `router`, 会额外增加耦合度, 同时这里不能直接使用 `useRouter`, 因为不在 `setup` 生命周期内
2. 在 `axios` 响应拦截器里抛出未授权错误, 在 `router.ts` 中使用[onError](https://router.vuejs.org/api/interfaces/Router.html#onError) 处理未授权错误

```ts
if (response.status === 401) {
	throw new UnauthorizedError('Unauthorized');
}
```

```ts
router.onError(error => {
	if(error instanceof UnauthorizedError) {
		// 跳转到登录页
		router.push('/login');
	}
})
```

```ts
const pinia = createPinia()
const app = createApp(App)

app.use(router)
app.use(pinia)

router.beforeEach((to) => {
  // ✅ This will work make sure the correct store is used for the
  // current running app
  const main = useMainStore(pinia)

  if (to.meta.requiresAuth && !main.isLoggedIn) return '/login'
})
```