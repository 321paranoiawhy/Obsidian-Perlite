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

# Basketball Hoop Loop

- [Codepen](https://codepen.io/chrisgannon/pen/NWzqyBY)

类似的圆环上小球环绕加载动画:

- [CSS3 环绕圆环 loading 小组件](https://www.cnblogs.com/btgyoyo/p/5854177.html)

# Heartbeat Preloader 

- [Heartbeat Preloader](https://codepen.io/RaulC/pen/KgWZjo)

# DNA Loading

- [DNA Loading](https://codepen.io/BjornRombaut/pen/gMgwgq)

# Sublime Text

- [Loader (Sublime Text Style)](https://codepen.io/OxyDesign/pen/OJoMyN)

# gradient loader

- [gradient loader](https://codepen.io/nazarelen/pen/ZpQgoW)

# 各网站加载效果

## Replit

## Discord

- [CSS Only Discord Loader](https://codepen.io/ElectroMantis/pen/ZaQxpm)

## Firefox

- [Mozilla Firefox Loader Icon](https://codepen.io/hlewis859/pen/KMVKoX)

```html
<body>
    <center>
        <div class="loader"></div>
    </center>
</body>
```

```css
body {
    background-color: #242424;
}

.loader {
    font-size: 10px;
    margin: 50px auto;
    text-indent: -9999em;
    width: 11em;
    height: 11em;
    border-radius: 50%;
    left: 0%;
    background: #ffffff;
    background: linear-gradient(
        to right,
        #ffffff 10%,
        rgba(255, 255, 255, 0) 42%
    );
    position: relative;
    animation: loading 1s infinite linear;
    transform: translateZ(0);
}

.loader:before {
    width: 50%;
    height: 50%;
    background: #ffffff;
    border-radius: 100% 0 0 0;
    position: absolute;
    top: 0;
    left: 0;
    content: "";
}
.loader:after {
    background: #242424;
    width: 75%;
    height: 75%;
    border-radius: 50%;
    content: "";
    margin: auto;
    position: absolute;
    top: 0;
    left: 0;
    bottom: 0;
    right: 0;
}

@keyframes loading {
    0% {
        transform: rotate(0deg);
    }
    100% {
        transform: rotate(360deg);
    }
}
```

- [Firefox loading dot (try)](https://codepen.io/notjb/pen/oEYeKK)

```html
<div class="circle"></div>
```

```css
/*
Trying o recreat Firfox Quantum tab loading animation
Graphic reference : http://gph.is/2E8WK29
*/

body {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  overflow: hidden;
}

.circle {
  display: block;
  width: 8px;
  height: 8px;
  background: #36a0ec;
  animation: 0.5s linear infinite alternate move;
  border-radius: 100%;
}

/*200%*/
/*@keyframes move {
  0%{transform: translateX(0%) scaleX(0.9);}
  20%{transform: translateX(40%) scaleX(1);}
  50%{transform: translateX(100%) scaleX(1.3);}
  80%{transform: translateX(160%) scaleX(1);}
  100%{transform: translateX(200%) scaleX(0.9);}
}*/

/*
400%
--
@source http://the12principles.tumblr.com
*/

@keyframes move {
  0% {
    transform: translateX(0%) scaleX(0.9);
  }
  20% {
    transform: translateX(80%) scaleX(1);
  }
  50% {
    transform: translateX(200%) scaleX(1.4);
  }
  80% {
    transform: translateX(320%) scaleX(1);
  }
  100% {
    transform: translateX(400%) scaleX(0.9);
  }
}
```

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