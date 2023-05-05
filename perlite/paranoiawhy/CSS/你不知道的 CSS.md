# column-count

对 `p` 标签分栏(两栏):

```css
p {
	column-count: 2;
}
```

# text-overflow

单行文本超出显示 `...`:

```css
.text-overflow {
  white-space: nowrap; 
  width: 200px; 
  overflow: hidden;
  text-overflow: ellipsis;
}
```

多行文本超出显示 `...`:

```css
```

# 输入框左右震动动画

```css
input:invalid{
      animation: shake 0.2s ease-in-out 0s 2;
      box-shadow: 0 0 0.4em red;
}
  @keyframes shake {
      0% { margin-left: 0rem; }
      25% { margin-left: 0.5rem; }
      75% { margin-left: -0.5rem; }
      100% { margin-left: 0rem; }
}
```

