**CSS权重：**

| 类型                 | 权重值   |
| -------------------- | -------- |
| !important           | infinity |
| 行间样式             | 1000     |
| id选择器             | 100      |
| 类、伪类、属性选择器 | 10       |
| 元素、伪元素         | 1        |
| 通配符*              | 0        |

1、!important

最高权重，

2、行间样式

3、id选择器

#### 4、类、伪类、属性选择器

**属性选择器：**

CSS **属性选择器**通过已经存在的属性名或属性值匹配元素。

```css
/* 存在title属性的<a> 元素 */
a[title] {
  color: purple;
}

/* 存在href属性并且属性值匹配"https://example.org"的<a> 元素 */
a[href="https://example.org"] {
  color: green;
}

/* 存在href属性并且属性值包含"example"的<a> 元素 */
a[href*="example"] {
  font-size: 2em;
}

/* 存在href属性并且属性值结尾是".org"的<a> 元素 */
a[href$=".org"] {
  font-style: italic;
}

/* 存在class属性并且属性值包含以空格分隔的"logo"的<a>元素 */
a[class~="logo"] {
  padding: 2px;
}
/* 存在class属性并且以t开头的<a>元素 */
div[class^="t"] {
    color: red;
}
```

切记这是属性选择器，而不是类：

比如：不匹配下面的div。

```css
        div[class^="t"] {
            color: red;
        }
```

```html
    <div class="aa ten">10</div>
```

**语法：**

（1）表示带有以 attr 命名的属性的元素。**——有某个属性**

```
[attr]
```

（2）表示带有以 attr 命名的属性，且属性值为 value 的元素。**——属性值为value的**

```
[attr=value]
```

（3）表示带有以 attr 命名的属性的元素，并且该属性是一个以空格作为分隔的值列表，其中至少有一个值为 value。**——其中一个属性值是value的**

```
[attr~=value]
```

（4）表示带有以 attr 命名的属性的元素，属性值为“value”或是以“value-”为前缀（"`-`"为连字符，Unicode 编码为 U+002D）开头。典型的应用场景是用来匹配语言简写代码（如 zh-CN，zh-TW 可以用 zh 作为 value）。

```
[attr|=value]
```

（5）表示带有以 attr 命名的属性，且属性值是以 value 开头的元素。**——以什么开头**

```
[attr^=value]
```

（6）表示带有以 attr 命名的属性，且属性值是以 value 结尾的元素。**——以什么结结尾**

```
[attr$=value]
```

（7）表示带有以 attr 命名的属性，且属性值至少包含一个 value 值的元素。**——只要带有某个片段**

```
[attr*=value]
```

（8）在属性选择器的右方括号前添加一个用空格隔开的字母 `i`（或 `I`），可以在匹配属性值时忽略大小写（支持 ASCII 字符范围之内的字母）。

```
[attr operator value i]
```

（9）在属性选择器的右方括号前添加一个用空格隔开的字母 `s`（或 `S`），可以在匹配属性值时区分大小写（支持 ASCII 字符范围之内的字母）。

```
[attr operator value s]
```



5、元素、伪元素



6、可以通过通配符修改浏览器默认样式，比如ul li的默认样式

