# 多彩标签

> [!tip]- 多彩标签
> ```css
> /* border-radius变量  */:root {  
>   /* 圆角-数字越大圆角越圆 */  /* --border-radius-wanzi: 0.5rem;  */  --border-radius-wanzi: 0.8rem!important;  
> }  
>   
> /* 样式1-七彩虹-不用的时候注释代码即可*/  
> :root {  
>   --font-color: white;  
>   --background-color-1: red;  
>   --background-color-2: orange;  
>   --background-color-3: #F4D00C;  
>   --background-color-4: green;  
>   --background-color-5: #00bbff;  
>   --background-color-6: blue;  
>   --background-color-7: purple;  
> }  
>   
> /* 样式2-Vue-渐变色-不用的时候注释代码即可 *//* :root {  
>   --font-color: white;  --background-color-1: #1f4d03;  --background-color-2: #548c14;  --background-color-3: #84bf41;  --background-color-4: #94d44a;  --background-color-5: #a1e751;  --background-color-6: #9fe251;  --background-color-7: #b2e07d;} */  
>   
> .tag:not(.token) {  
>   background-color: var(--text-accent);  
>   border: none;  
>   color: var(--font-color);  
>   font-size: 0.875rem; /* 14px 调整在v1.0.0 版本中的样式 */  /* padding: 1px 8px; */  padding: 2px 8px; /* 2022-08-10 12:57:05 */  
>   text-align: center;  
>   text-decoration: none;  
>   display: inline-block;  
>   margin: 0px 0px;  
>   cursor: pointer;  
>   border-radius: var(--border-radius-wanzi);  
> }  
>   
> /* 配色设置 *//* 设置.markdown-reading-view 下第1个.tag背景色*/  
> .markdown-reading-view .tag:not(.token):first-child {  
>   /* 背景颜色为变量 1 */  background-color: var(--background-color-1);  
> }  
>   
> /* 设置.markdown-reading-view 下第2个.tag背景色*/  
> .markdown-reading-view .tag:not(.token):nth-child(2) {  
>   /* 背景颜色为变量 2 */  background-color: var(--background-color-2);  
> }  
>   
> /* 设置.markdown-reading-view 下第3个.tag背景色*/  
> .markdown-reading-view .tag:not(.token):nth-child(3) {  
>   /* 背景颜色为变量 3 */  background-color: var(--background-color-3);  
> }  
>   
> /* 设置.markdown-reading-view 下第4个.tag背景色*/  
> .markdown-reading-view .tag:not(.token):nth-child(4) {  
>   /* 背景颜色为变量 4 */  background-color: var(--background-color-4);  
> }  
>   
> /* 设置.markdown-reading-view 下第5个.tag背景色*/  
> .markdown-reading-view .tag:not(.token):nth-child(5) {  
>   /* 背景颜色为变量 5 */  background-color: var(--background-color-5);  
> }  
>   
> /* 设置.markdown-reading-view 下第6个.tag背景色 */.markdown-reading-view .tag:not(.token):nth-child(6) {  
>   /* 背景颜色为变量 6 */  background-color: var(--background-color-6);  
> }  
>   
> /* 设置.markdown-reading-view 下第7个.tag背景色*/  
> .markdown-reading-view .tag:not(.token):nth-child(7) {  
>   /* 背景颜色为变量 7 */  background-color: var(--background-color-7);  
> }
> ```

> [!caution]
> 此 `CSS` 代码片段仅适用于部分主题如 `Blue Topaz`, 不适用于 `Atom` 主题。

- [CSS片段-标签多彩小丸子](https://coffeetea.top/zh/css-snippets/%E6%A0%87%E7%AD%BE%E5%A4%9A%E5%BD%A9%E5%B0%8F%E4%B8%B8%E5%AD%90.html)

# 多彩文件夹

```css
.nav-folder-title:nth-child(1) {
  background-color: red;
}
```

# 图片水平居中

> [!tip] 图片水平居中
> ```css
> img {  
> 	display: block !important;  
> 	margin-left: auto !important;  
> 	margin-right: auto !important;  
> }  
>       
>  .markdown-source-view.mod-cm6 .cm-content > * {  
> 	margin: auto auto !important;  
> }
> ```

# 预览模式下标题前显示 `H1 ~ H6`

> [!tip]- 预览模式下标题前显示 `H1 ~ H6`
> ```css
> .is-live-preview
>   div.cm-contentContainer
>   div.HyperMD-header.HyperMD-header-1.cm-line::before {
>   content: "H1";
>   color: #6b6d6f;
>   margin-right: 0px;
>   font-size: 0.8rem;
>   margin-right: 5px;
>   font-weight: normal;
> }
> 
> .is-live-preview
>   div.cm-contentContainer
>   div.HyperMD-header.HyperMD-header-2.cm-line::before {
>   content: "H2";
>   color: #6b6d6f;
>   margin-right: 0px;
>   font-size: 0.8rem;
>   margin-right: 5px;
>   font-weight: normal;
> }
> 
> .is-live-preview
>   div.cm-contentContainer
>   div.HyperMD-header.HyperMD-header-3.cm-line::before {
>   content: "H3";
>   color: #6b6d6f;
>   margin-right: 0px;
>   font-size: 0.8rem;
>   margin-right: 5px;
>   font-weight: normal;
> }
> 
> .is-live-preview
>   div.cm-contentContainer
>   div.HyperMD-header.HyperMD-header-4.cm-line::before {
>   content: "H4";
>   color: #6b6d6f;
>   margin-right: 0px;
>   font-size: 0.8rem;
>   margin-right: 5px;
>   font-weight: normal;
> }
> 
> .is-live-preview
>   div.cm-contentContainer
>   div.HyperMD-header.HyperMD-header-5.cm-line::before {
>   content: "H5";
>   color: #6b6d6f;
>   margin-right: 0px;
>   font-size: 0.8rem;
>   margin-right: 5px;
>   font-weight: normal;
> }
> 
> .is-live-preview
>   div.cm-contentContainer
>   div.HyperMD-header.HyperMD-header-6.cm-line::before {
>   content: "H6";
>   color: #6b6d6f;
>   margin-right: 0px;
>   font-size: 0.8rem;
>   margin-right: 5px;
>   font-weight: normal;
> }
> ```
	
# 水平分割线样式

> [!caution]
> `hr` 元素的 `overflow` 属性默认值为 `hidden`, 须通过 `CSS` 样式将其值设为 `visible` 或 `initial`。

## Square

- [666，看hr标签实现分隔线如何玩出花 - 张鑫旭](https://www.zhangxinxu.com/wordpress/2021/05/css-html-hr/)

> [!tip]- Square
> ```css
> hr {
>   border: 0;
>   color: #d0d0d5;
>   background: linear-gradient(currentColor, currentColor) no-repeat center;
>   background-size: 100% 1px;
> }
> 
> hr::before {
>   content: "";
>   display: block;
>   width: 0.75em;
>   height: 0.75em;
>   transform: rotate(45deg);
>   background-color: currentColor;
>   margin: 3px auto;
> }
> ```

## Circle

> [!tip]- Circle
> ```css
> hr {
>   border: 0;
>   color: #d0d0d5;
>   background: linear-gradient(currentColor, currentColor) no-repeat center;
>   background-size: 100% 1px;
> }
> 
> hr::before {
>   content: "";
>   display: block;
>   width: 0.75em;
>   height: 0.75em;
>   border-radius: 50%;
>   background-color: currentColor;
>   margin: auto;
> }
> ```

## Bootstrap

![[../../Attachments/bootstrap-horizontal-divider.png]]

> [!tip]- Bootstrap
> ```css
> .hr.cm-line hr,
> .markdown-rendered hr {
>   position: relative;
>   overflow: visible;
>   border-bottom: 1px solid #f0f0f0;
>   margin-bottom: 30px;
>   margin-top: 30px;
> }
> 
> .hr.cm-line hr::before,
> .markdown-rendered hr::before {
>   position: absolute;
>   content: " ";
>   width: 30px;
>   height: 30px;
>   border: 1px solid #f0f0f0;
>   left: 50%;
>   margin-left: -15px;
>   top: 50%;
>   background: #fff;
>   margin-top: -15px;
>   -webkit-transform: rotate(45deg);
>   -moz-transform: rotate(45deg);
>   -ms-transform: rotate(45deg);
>   transform: rotate(45deg);
> }
> 
> .hr.cm-line hr::after,
> .markdown-rendered hr::after {
>   position: absolute;
>   content: " ";
>   width: 20px;
>   height: 20px;
>   border: 1px solid #2ca5b9;
>   left: 50%;
>   margin-left: -10px;
>   top: 50%;
>   background: #2ca5b9;
>   margin-top: -10px;
>   -webkit-transform: rotate(45deg);
>   -moz-transform: rotate(45deg);
>   -ms-transform: rotate(45deg);
>   transform: rotate(45deg);
> }
> ```

- 选择器不可直接使用 `hr`, 否则会影响 `obsidian` 软件界面其他地方的水平分割线样式;
- 编辑模式 (`Editing View`) 下对应的选择器为 `.hr.cm-line hr`;
- 预览模式 (`Reading View`) 下对应的选择器为 `.markdown-rendered hr`。

[Bootstrap Horizontal Divider - Codepen](https://codepen.io/tlongren/pen/RGLrve)

## Lightning

```css
```

## Star Icon

```html
<div class="astrodivider">
  <div class="astrodividermask"></div>
  <span>
	  <i>&#10038;</i>
  </span>
</div>
```

> [!tip]- Pure CSS Horizontal Divider With Star Icon
> ```css
> .astrodivider {
>   margin: 64px auto;
>   max-width: 100%;
>   position: relative;
> }
> 
> .astrodividermask {
>   overflow: hidden;
>   height: 20px;
> }
> 
> .astrodividermask:after {
>   content: "";
>   display: block;
>   margin: -25px auto 0;
>   width: 100%;
>   height: 25px;
>   border-radius: 125px / 12px;
>   box-shadow: 0 0 8px #049372;
> }
> .astrodivider span {
>   width: 50px;
>   height: 50px;
>   position: absolute;
>   bottom: 100%;
>   margin-bottom: -25px;
>   left: 50%;
>   margin-left: -25px;
>   border-radius: 100%;
>   box-shadow: 0 2px 4px #4fb39c;
>   background: #fff;
> }
> .astrodivider i {
>   position: absolute;
>   top: 4px;
>   bottom: 4px;
>   left: 4px;
>   right: 4px;
>   border-radius: 100%;
>   border: 1px dashed #68beaa;
>   text-align: center;
>   line-height: 40px;
>   font-style: normal;
>   color: #049372;
> }
> ```

[Pure CSS Horizontal Divider With Star Icon - Codepen](https://codepen.io/isabelc/pen/MmrJgx)

## `Google Material Design`

```html
<svg _ngcontent-pah-c40="" aria-hidden="true" width="100%" height="8" fill="none" xmlns="http://www.w3.org/2000/svg"><pattern _ngcontent-pah-c40="" id="a" width="91" height="8" patternUnits="userSpaceOnUse"><g _ngcontent-pah-c40="" clip-path="url(#clip0_2426_11367)"><path _ngcontent-pah-c40="" d="M114 4c-5.067 4.667-10.133 4.667-15.2 0S88.667-.667 83.6 4 73.467 8.667 68.4 4 58.267-.667 53.2 4 43.067 8.667 38 4 27.867-.667 22.8 4 12.667 8.667 7.6 4-2.533-.667-7.6 4s-10.133 4.667-15.2 0S-32.933-.667-38 4s-10.133 4.667-15.2 0-10.133-4.667-15.2 0-10.133 4.667-15.2 0-10.133-4.667-15.2 0-10.133 4.667-15.2 0-10.133-4.667-15.2 0-10.133 4.667-15.2 0-10.133-4.667-15.2 0-10.133 4.667-15.2 0-10.133-4.667-15.2 0-10.133 4.667-15.2 0-10.133-4.667-15.2 0-10.133 4.667-15.2 0-10.133-4.667-15.2 0-10.133 4.667-15.2 0-10.133-4.667-15.2 0-10.133 4.667-15.2 0-10.133-4.667-15.2 0-10.133 4.667-15.2 0-10.133-4.667-15.2 0-10.133 4.667-15.2 0-10.133-4.667-15.2 0-10.133 4.667-15.2 0-10.133-4.667-15.2 0-10.133 4.667-15.2 0" stroke="#E1E3E1" stroke-linecap="square"></path></g></pattern><rect _ngcontent-pah-c40="" width="100%" height="100%" fill="url(#a)"></rect></svg>
```

- [Material Design 3](https://m3.material.io/)