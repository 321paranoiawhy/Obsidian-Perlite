# Heading

[[Sticky Footers]]

## 忽略 h1 标题, 仅对 h2 ~ h6 标题进行编号

通常一篇文章仅一个 `h1` 标题且无需编号, 仅对 `h2 ~ h6` 标题进行编号:

```css
body {
  counter-reset: h2;
}
h2 {
  counter-reset: h3;
}
h3 {
  counter-reset: h4;
}
h4 {
  counter-reset: h5;
}
h5 {
  counter-reset: h6;
}


h2:before {
  counter-increment: h2;
  content: counter(h2) ". ";
}
h3:before {
  counter-increment: h3;
  content: counter(h2) "." counter(h3) ". ";
}
h4:before {
  counter-increment: h4;
  content: counter(h2) "." counter(h3) "." counter(h4) ". ";
}
h5:before {
  counter-increment: h5;
  content: counter(h2) "." counter(h3) "." counter(h4) "." counter(h5) ". ";
}
h6:before {
  counter-increment: h6;
  content: counter(h2) "." counter(h3) "." counter(h4) "." counter(h5) "."
    counter(h6) ". ";
}
```

## h1 ~ h6 标题均进行编号

如果文章有多个 `h1` 标题且各标题均需编号:

```css
body {
  counter-reset: h1;
}
h1 {
  counter-reset: h2;
}
h2 {
  counter-reset: h3;
}
h3 {
  counter-reset: h4;
}
h4 {
  counter-reset: h5;
}
h5 {
  counter-reset: h6;
}


h1:before {
  counter-increment: h1;
  content: counter(h1) ". ";
}
h2:before {
  counter-increment: h2;
  content: counter(h1) "." counter(h2) ". ";
}
h3:before {
  counter-increment: h3;
  content: counter(h1) "." counter(h2) "." counter(h3) ". ";
}
h4:before {
  counter-increment: h4;
  content: counter(h1) "." counter(h2) "." counter(h3) "." counter(h4) ". ";
}
h5:before {
  counter-increment: h5;
  content: counter(h1) "." counter(h2) "." counter(h3) "." counter(h4) "."
    counter(h5) ". ";
}
h6:before {
  counter-increment: h6;
  content: counter(h1) "." counter(h2) "." counter(h3) "." counter(h4) "."
    counter(h5) "." counter(h6) ". ";
}
```

## 不需要编号的标题 

添加 `no-count` 类名:

```css
h1.nocount:before,
h2.nocount:before,
h3.nocount:before,
h4.nocount:before,
h5.nocount:before,
h6.nocount:before {
  content: "";
  counter-increment: none;
}
```

不需要编号的标题如:
- Introduction
- Conclusion
- ...

## 更改编号格式

可将上述 `CSS` 代码中的 `.` 改为 `-` 或 `/` :

- 1.1.1.1
- 1-1-1-1
- 1/1/1/1

## Reference

- [Automatic Heading Numbers with CSS](https://philarcher.org/diary/2013/headingnumbers/)
- [Numbered headings made with CSS counter](https://nikitahl.com/numbered-headings-with-css-counter)
- [CSS, auto numbering elements : headings, lists, pagination](https://www.sqlpac.com/en/documents/html-css-auto-numbering-elements-counters.htm)
- [利用 CSS 对标题进行自动编号](https://razonyang.com/zh-hans/notes/css/numberify-headings/)
- [3 段 h1 标题 CSS 美化代码](https://www.wdzzz.com/jiaocheng/css/2020-08-14/1528.html)
- [Example of a nested counter](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Counter_Styles/Using_CSS_counters#example_of_a_nested_counter)

# ul/ol li

## ul li

```css
ul {
  counter-reset: section; /* Creates a new instance of the
                             section counter with each ul
                             element */
  list-style-type: none;
}

ul li::before {
  counter-increment: section; /* Increments only this instance
                                            of the section counter */
  content: counters(section, ".") " "; /* Combines the values of all instances
                                          of the section counter, separated
                                          by a period */
}
```

```html
<ul>
  <li>item</li>          <!-- 1     -->
  <li>item               <!-- 2     -->
    <ul>
      <li>item</li>      <!-- 2.1   -->
      <li>item</li>      <!-- 2.2   -->
      <li>item           <!-- 2.3   -->
        <ul>
          <li>item</li>  <!-- 2.3.1 -->
          <li>item</li>  <!-- 2.3.2 -->
        </ul>
        <ul>
          <li>item</li>  <!-- 2.3.1 -->
          <li>item</li>  <!-- 2.3.2 -->
          <li>item</li>  <!-- 2.3.3 -->
        </ul>
      </li>
      <li>item</li>      <!-- 2.4   -->
    </ul>
  </li>
  <li>item</li>          <!-- 3     -->
  <li>item</li>          <!-- 4     -->
</ul>
<ul>
  <li>item</li>          <!-- 1     -->
  <li>item</li>          <!-- 2     -->
</ul>
```

## ol li

- [Example of a nested counter](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Counter_Styles/Using_CSS_counters#example_of_a_nested_counter)

```css
ol {
  counter-reset: section; /* Creates a new instance of the
                             section counter with each ol
                             element */
  list-style-type: none;
}

ol li::before {
  counter-increment: section; /* Increments only this instance
                                            of the section counter */
  content: counters(section, ".") " "; /* Combines the values of all instances
                                          of the section counter, separated
                                          by a period */
}
```

```html
<ol>
  <li>item</li>          <!-- 1     -->
  <li>item               <!-- 2     -->
    <ol>
      <li>item</li>      <!-- 2.1   -->
      <li>item</li>      <!-- 2.2   -->
      <li>item           <!-- 2.3   -->
        <ol>
          <li>item</li>  <!-- 2.3.1 -->
          <li>item</li>  <!-- 2.3.2 -->
        </ol>
        <ol>
          <li>item</li>  <!-- 2.3.1 -->
          <li>item</li>  <!-- 2.3.2 -->
          <li>item</li>  <!-- 2.3.3 -->
        </ol>
      </li>
      <li>item</li>      <!-- 2.4   -->
    </ol>
  </li>
  <li>item</li>          <!-- 3     -->
  <li>item</li>          <!-- 4     -->
</ol>
<ol>
  <li>item</li>          <!-- 1     -->
  <li>item</li>          <!-- 2     -->
</ol>
```

- [Codepen Demo](https://codepen.io/paraoiawhy/pen/MWqJLpX)

# Pagination

```html
<ul class="paging">
	<li><a data-nocount href="…">&lt;</a></li>
	<li><a href="#"></a></li>
	<li><a href="#"></a></li>
	<li><a href="#"></a></li>
	<li><a href="#"></a></li>
	<li><a data-nocount href="…">&gt;</a></li>
</ul>
```

```css
:root {
    --start-toolbar-paging: 3;
}

ul[class*="paging"] {
    display: flex;
    column-gap: 12px;
    justify-content: center;
    padding: 0;
    list-style-type: none;
    counter-reset: pgcounter var(--start-toolbar-paging);
}

ul[class*="paging"] li a:not([data-nocount])::before {
	  counter-increment: pgcounter;
	  content: counter(pgcounter);
}

ul li a {
  text-decoration: none;
}
```

- [Codepen Demo](https://codepen.io/paraoiawhy/pen/gOdgqyx)