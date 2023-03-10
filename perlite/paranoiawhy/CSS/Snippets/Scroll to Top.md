# salesforce

`body` 标签下内容:

```html
<div>1</div>
<div>2</div>
<div>3</div>
<div>4</div>
<div>5</div>
<div>6</div>
<div>7</div>
<div>8</div>
<div>9</div>
<div>10</div>

<button class="btn-toggle-round scroll-top js-scroll-top is-active" type="button" title="Scroll to top">
  <svg class="progress-circle" width="100%" height="100%" viewBox="-1 -1 102 102">
    <path d="M50,1 a49,49 0 0,1 0,98 a49,49 0 0,1 0,-98" style="transition: stroke-dashoffset 10ms linear 0s; stroke-dasharray: 307.919, 307.919; stroke-dashoffset: 102.932;"></path>
  </svg>
  <svg xmlns="http://www.w3.org/2000/svg" class="icon icon-tabler icon-tabler-arrow-up" width="24" height="24" viewBox="0 0 24 24" stroke-width="1.5" stroke="cuurentColor" fill="none" stroke-linecap="round" stroke-linejoin="round">
    <path stroke="none" d="M0 0h24v24H0z" fill="none"></path>
    <line x1="12" y1="5" x2="12" y2="19"></line>
    <line x1="18" y1="11" x2="12" y2="5"></line>
    <line x1="6" y1="11" x2="12" y2="5"></line>
  </svg>
</button>
```

`CSS` 样式:

```css
body {
  position: relative;
  scroll-behavior: smooth;
  overflow-y: auto;
}

div {
  height: 300px;
  text-align: center;
}

button {
  -webkit-text-size-adjust: 100%;
  -webkit-font-smoothing: antialiased;
  --d: 20px;
  --d-th: 1.6px;
  --h-th: 1px;
  --h: 30px;
  --footnotation-color: var(--tinged-white-accent-color);
  --architects-line-color: var(--extra-bright-accent-color);
  --popup-box-bg-color: rgb(239, 239, 239);
  --footnote-font-size: 11.5px;
  --footnote-line-height: 14px;
  font: inherit;
  margin: 0;
  overflow: visible;
  -webkit-appearance: button;
  text-align: center;
  font-size: 11px;
  font-weight: 600;
  line-height: 38px;
  letter-spacing: 0.1rem;
  text-transform: uppercase;
  text-decoration: none;
  white-space: nowrap;
  box-sizing: border-box;
  margin-bottom: 1rem;
  --ghost-accent-color: royalblue;
  position: fixed;
  z-index: 50;
  padding: 0;
  right: 20px;
  bottom: 20px;
  height: 46px;
  width: 46px;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 50%;
  transition: all 0.4s ease;
  border: none;
  box-shadow: inset 0 0 0 2px #ccc;
  color: #ccc;
  background-color: #fff;
  margin-right: 1rem;
  opacity: 1;
  visibility: visible;
  transform: translateY(0);
}
.progress-circle {
  -webkit-text-size-adjust: 100%;
  -webkit-font-smoothing: antialiased;
  --d: 20px;
  --d-th: 1.6px;
  --h-th: 1px;
  --h: 30px;
  --footnotation-color: var(--tinged-white-accent-color);
  --architects-line-color: var(--extra-bright-accent-color);
  --popup-box-bg-color: rgb(239, 239, 239);
  --footnote-font-size: 11.5px;
  --footnote-line-height: 14px;
  font: inherit;
  text-align: center;
  font-size: 11px;
  font-weight: 600;
  line-height: 38px;
  letter-spacing: 0.1rem;
  text-transform: uppercase;
  white-space: nowrap;
  --ghost-accent-color: royalblue;
  cursor: pointer;
  color: #ccc;
  visibility: visible;
  width: 100%;
  height: 100%;
  box-sizing: inherit;
  overflow: hidden;
}

.progress-circle path {
  -webkit-text-size-adjust: 100%;
  -webkit-font-smoothing: antialiased;
  --d: 20px;
  --d-th: 1.6px;
  --h-th: 1px;
  --h: 30px;
  --footnotation-color: var(--tinged-white-accent-color);
  --architects-line-color: var(--extra-bright-accent-color);
  --popup-box-bg-color: rgb(239, 239, 239);
  --footnote-font-size: 11.5px;
  --footnote-line-height: 14px;
  font: inherit;
  text-align: center;
  font-size: 11px;
  font-weight: 600;
  line-height: 38px;
  letter-spacing: 0.1rem;
  text-transform: uppercase;
  white-space: nowrap;
  --ghost-accent-color: royalblue;
  cursor: pointer;
  color: #ccc;
  visibility: visible;
  d: path("M 50 1 a 49 49 0 0 1 0 98 a 49 49 0 0 1 0 -98");
  box-sizing: inherit;
  fill: none;
  stroke: #333;
  stroke-width: 4;
  transition: stroke-dashoffset 10ms linear 0s;
  stroke-dasharray: 307.919, 307.919;
  stroke-dashoffset: 102.932;
}

.icon-tabler-arrow-up {
  -webkit-text-size-adjust: 100%;
  -webkit-font-smoothing: antialiased;
  --d: 20px;
  --d-th: 1.6px;
  --h-th: 1px;
  --h: 30px;
  --footnotation-color: var(--tinged-white-accent-color);
  --architects-line-color: var(--extra-bright-accent-color);
  --popup-box-bg-color: rgb(239, 239, 239);
  --footnote-font-size: 11.5px;
  --footnote-line-height: 14px;
  font: inherit;
  text-align: center;
  font-size: 11px;
  font-weight: 600;
  line-height: 38px;
  letter-spacing: 0.1rem;
  text-transform: uppercase;
  white-space: nowrap;
  --ghost-accent-color: royalblue;
  cursor: pointer;
  color: #ccc;
  visibility: visible;
  width: 24;
  height: 24;
  fill: none;
  stroke-linecap: round;
  stroke-linejoin: round;
  box-sizing: inherit;
  overflow: hidden;
  position: absolute;
  stroke-width: 2px;
  stroke: #333;
}
```

`JavaScript` 代码:

```js
const scrollTopBtn = document.querySelector(".js-scroll-top");
if (scrollTopBtn) {
  scrollTopBtn.onclick = () => {
    window.scrollTo({
      top: 0,
      behavior: "smooth"
    });
  };

  const progressPath = document.querySelector(".scroll-top path");
  const pathLength = progressPath.getTotalLength();
  progressPath.style.transition = progressPath.style.WebkitTransition = "none";
  progressPath.style.strokeDasharray = `${pathLength} ${pathLength}`;
  progressPath.style.strokeDashoffset = pathLength;
  progressPath.getBoundingClientRect();
  progressPath.style.transition = progressPath.style.WebkitTransition =
    "stroke-dashoffset 10ms linear";
  const updateProgress = function () {
    const scroll =
      window.scrollY ||
      window.scrollTopBtn ||
      document.documentElement.scrollTopBtn;

    const docHeight = Math.max(
      document.body.scrollHeight,
      document.documentElement.scrollHeight,
      document.body.offsetHeight,
      document.documentElement.offsetHeight,
      document.body.clientHeight,
      document.documentElement.clientHeight
    );

    const windowHeight = Math.max(
      document.documentElement.clientHeight,
      window.innerHeight || 0
    );

    const height = docHeight - windowHeight;
    var progress = pathLength - (scroll * pathLength) / height;
    progressPath.style.strokeDashoffset = progress;
  };

  updateProgress();
  const offset = 100;

  window.addEventListener(
    "scroll",
    function (event) {
      updateProgress();

      // Scroll back to top
      const scrollPos =
        window.scrollY ||
        window.scrollTopBtn ||
        document.getElementsByTagName("html")[0].scrollTopBtn;
      scrollPos > offset
        ? scrollTopBtn.classList.add("is-active")
        : scrollTopBtn.classList.remove("is-active");
    },
    false
  );
}
```

[Codepen Demo](https://codepen.io/paraoiawhy/pen/yLxPYya)