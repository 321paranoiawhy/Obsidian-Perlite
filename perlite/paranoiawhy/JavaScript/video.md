# timeupdate

实时获取视频播放进度, 单位为 `s` (秒)

- [HTMLMediaElement: timeupdate event](https://developer.mozilla.org/en-US/docs/Web/API/HTMLMediaElement/timeupdate_event)
- [bindtimeupdate - 微信小程序 video 组件](https://developers.weixin.qq.com/miniprogram/dev/component/video.html)

	浏览器中 `timeupdate` 事件触发频率与系统负载直接相关, 频率在 `4 HZ ~ 66 HZ`, 分别对应 `250 ms` 和 `15.15 ms`。

	微信小程序的 `bindtimeupdate` 事件触发频率则始终为 `250 ms`。

## 微信小程序

```js
onTimeUpdate(e) {
	console.log(e.datail.currentTime)
}
```

微信小程序使用 `js` 动态插入自定义组件:

- [支持组件动态插入](https://wxopen.club/topic/5e2ec0b4f2cd9aae7acbd1fd)
- [微信小程序动态加载组件](https://juejin.cn/s/%E5%BE%AE%E4%BF%A1%E5%B0%8F%E7%A8%8B%E5%BA%8F%E5%8A%A8%E6%80%81%E5%8A%A0%E8%BD%BD%E7%BB%84%E4%BB%B6)
- [自定义组件 - Component 构造器](https://developers.weixin.qq.com/miniprogram/dev/framework/custom-component/component.html)

> [!warning]
> 注意：在组件 `wxss` 中不应使用 `ID` 选择器、属性选择器和标签名选择器。
> 推荐使用类选择器。

微信小程序 `video` 标签默认宽度为 `300 px`, 默认高度为 `225px`, 可通过 `wxss` 设置其宽高。

`2.4.0` 起 `video` 标签支持**同层渲染**, [详见 - 原生组件的使用限制](https://developers.weixin.qq.com/miniprogram/dev/component/native-component.html#%E5%8E%9F%E7%94%9F%E7%BB%84%E4%BB%B6%E7%9A%84%E4%BD%BF%E7%94%A8%E9%99%90%E5%88%B6)

[微信小程序图片加载优化](https://jelly.jd.com/article/6006b1045b6c6a01506c87d4)
[京喜小程序首页瘦身实践——给小程序再减重30%的秘密](https://jelly.jd.com/article/5fbfa6e9cff6b301458392c3)

> [!tip]
> 微信小程序平台差异:
> - `JavaScript` 语法差异: [ES6 转 ES5](https://developers.weixin.qq.com/miniprogram/dev/devtools/codecompile.html#es6-%E8%BD%AC-es5)
> - `WXSS` 样式差异: [样式补全](https://developers.weixin.qq.com/miniprogram/dev/devtools/codecompile.html#%E6%A0%B7%E5%BC%8F%E8%A1%A5%E5%85%A8)

微信小程序中使用 `TypeScript` 和 `less / sass` : [原生支持 TypeScript](https://developers.weixin.qq.com/miniprogram/dev/devtools/compilets.html)

[vant 微信小程序 popup](https://vant-contrib.gitee.io/vant-weapp/#/popup)

## uniapp APP

```js
onTimeUpdate(e) {
	console.log(e.datail.datail.currentTime)
}
```

[详见](https://ask.dcloud.net.cn/question/91420)

# 判断横竖屏

- [探讨判断横竖屏的最佳实现](https://jelly.jd.com/article/6006b1045b6c6a01506c87db)