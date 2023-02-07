#Loading #Animation
# Dual ring spinner

```html
<div class="loading">
  <div class="loader"></div>
</div>
```

> [!tip]- Dual ring spinner
> ```css
> .loading {
>   display: flex;
>   justify-content: center;
>   align-items: center;
>   margin: 0;
>   position: absolute;
>   top: 50%;
>   left: 50%;
>   -ms-transform: translate(-50%, -50%);
>   transform: translate(-50%, -50%);
> }
> 
> .loader {
>   border: 16px solid #f3f3f3;
>   border-radius: 50%;
>   border: 15px solid;
>   border-top: 16px solid blue;
>   border-right: 16px solid white;
>   border-bottom: 16px solid blue;
>   border-left: 16px solid white;
>   width: 120px;
>   height: 120px;
>   -webkit-animation: spin 2s linear infinite;
>   animation: spin 2s linear infinite;
> }
> 
> @-webkit-keyframes spin {
>   0% {
>     -webkit-transform: rotate(0deg);
>   }
>   100% {
>     -webkit-transform: rotate(360deg);
>   }
> }
> 
> @keyframes spin {
>   0% {
>     transform: rotate(0deg);
>   }
>   100% {
>     transform: rotate(360deg);
>   }
> }
> ```

[Codepen](https://codepen.io/paraoiawhy/pen/vYaNzXE)

# Flat Preloader

```html
<div class="load">
  <hr/><hr/><hr/><hr/>
</div>
```

> [!tip]- Flat Preloader
> ```css
> body {
>   background: #ecf0f1;
> }
> 
> .load {
>   position: absolute;
>   top: 50%;
>   left: 50%;
>   transform: translate(-50%, -50%);
>   /*change these sizes to fit into your project*/
>   width: 100px;
>   height: 100px;
> }
> .load hr {
>   border: 0;
>   margin: 0;
>   width: 40%;
>   height: 40%;
>   position: absolute;
>   border-radius: 50%;
>   animation: spin 2s ease infinite;
> }
> 
> .load :first-child {
>   background: #19a68c;
>   animation-delay: -1.5s;
> }
> .load :nth-child(2) {
>   background: #f63d3a;
>   animation-delay: -1s;
> }
> .load :nth-child(3) {
>   background: #fda543;
>   animation-delay: -0.5s;
> }
> .load :last-child {
>   background: #193b48;
> }
> 
> @keyframes spin {
>   0%,
>   100% {
>     transform: translate(0);
>   }
>   25% {
>     transform: translate(160%);
>   }
>   50% {
>     transform: translate(160%, 160%);
>   }
>   75% {
>     transform: translate(0, 160%);
>   }
> }
> 
> ```

[Codepen](https://codepen.io/zerospree/pen/XWaGER)

# Reference

* [loading.io](https://loading.io/)
* [CSS Loaders](https://cssloaders.github.io/)
* [CSS3 Loader & Spinners](https://codepen.io/vineethtrv/pen/NWxZqMM)
* [How To Create a Loader](https://www.w3schools.com/howto/howto_css_loader.asp)
* [153 CSS Spinners](https://freefrontend.com/css-loaders/)
* [80+ Best Pure CSS Loading Spinners For Front-end Developers](https://365webresources.com/best-pure-css-loading-spinners/)
* [50 inspiring Loading Animations](https://webdeasy.de/en/css-loading-animations/)
* [I made 100 CSS loaders for your next project](https://dev.to/afif/i-made-100-css-loaders-for-your-next-project-4eje)
* [纯 css 实现117个Loading效果 (上)](https://juejin.cn/post/7037036742985121800)
* [纯 css 实现117个Loading效果 (中)](https://juejin.cn/post/7037636080539009038)
* [纯 css 实现117个Loading效果 (下)](https://juejin.cn/post/7037660617779445796)
* [Spinkit](https://tobiasahlin.com/spinkit/)
* [CSS Only Discord Loader](https://codepen.io/ElectroMantis/pen/ZaQxpm)