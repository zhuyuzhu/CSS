# 伪元素（pseudo-element）

伪元素开头为双冒号`::`

```
::pseudo-element-name
```

> **备注：**一些早期的伪元素曾使用单冒号的语法，所以你可能会在代码或者示例中看到。现代的浏览器为了保持后向兼容，支持早期的带有单双冒号语法的伪元素。

 由`::before` 和`::after` 生成的伪元素 [包含在元素格式框内](https://www.w3.org/TR/CSS2/generate.html#before-after-content)， 因此不能应用在*[替换元素上](https://developer.mozilla.org/en-US/docs/Web/CSS/Replaced_element)，* 比如img 或 br元素。行元素内也可以有伪元素。`::before` 和 `::after`可以通`content`属性一起使用，给伪元素中插入内容。

还可以使用`::before` 和 `::after`来清除浮动流，必须是具有块属性的元素才可以清除浮动流。

```css
::before {
            content: '';
            display: inline-block;
            clear: both;
        }
```

### 1、::after 或 :after

`::after`用来创建一个伪元素，**作为已选中元素的最后一个子元素。**——**特点：被选元素的最后一个子元素**

通常会配合[`content`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/content)属性来为该元素添加装饰内容。这个虚拟元素默认是**行内元素**。——**特点 display:inline**

::after表示法是在CSS 3中引入的，::符号是用来区分伪类和伪元素的。支持CSS3的浏览器同时也都支持CSS2中引入的表示法 :after。

>  **注:** IE8仅支持`:after。`

**特点：不是dom的内容，无法被鼠标选中**

示例：

```html
    <p class="boring-text">这是些无聊的文字</p>
    <p>这是不无聊也不有趣的文字</p>
    <p class="exciting-text">在MDN上做贡献简单又轻松。
        按右上角的编辑按钮添加新示例或改进旧示例！</p>
```

```css
    .exciting-text::after {
        content: "<- 让人兴兴兴奋!";
        color: green;
    }
    .boring-text::after {
        content: "<- 无聊!";
        color: red;
    }
```



**示例：提示词用法**

```html
    <p>这是上面代码的实现<br />
        我们有一些 <span data-descr="collection of words and punctuation">文字</span> 有一些
        <span data-descr="small popups which also hide again">提示</span>。<br />
        把鼠标放上去<span data-descr="not to be taken literally">看看</span>.
    </p>
```

```css
        span[data-descr] {
            position: relative;
            text-decoration: underline;
            color: #00F;
            cursor: help;
        }

        span[data-descr]:hover::after {
            content: attr(data-descr);
            position: absolute;
            left: 0;
            top: 24px;
            min-width: 200px;
            border: 1px #aaaaaa solid;
            border-radius: 10px;
            background-color: #ffffcc;
            padding: 12px;
            color: #000000;
            font-size: 14px;
            z-index: 1;
        }
```

关于伪元素的特点：写在类后面，即该类修饰的元素生效时，伪元素生效。

当span[data-descr]:hover生效时，添加伪元素::after

> 文字、提示、看看   这三个span标签，position: relative，而他们的伪元素，position：absolute，根据父级span进行定位。且z-index：1，让其显示的更靠前。

**补充：attr() 方法；**

**注意:** `attr()` 理论上能用于所有的CSS属性但目前支持的仅有伪元素的 [`content`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/content) 属性，其他的属性和高级特性目前是实验性的

译者注：如果发现浏览器兼容表里attr()的高级用法依旧没有良好的支持的话，本文大部分内容都是纸上谈兵

CSS表达式 `attr()` 用来获取选择到的元素的某一HTML属性值，并用于其样式。它也可以用于伪元素，属性值采用伪元素所依附的元素。

兼容性：IE8



https://developer.mozilla.org/zh-CN/docs/Web/CSS/::after



### 2、::before 或 :before

**`::before`** 创建一个[伪元素](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-elements)，其将成为匹配选中的元素的**第一个子元素**。

常通过 [`content`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/content) 属性来为一个元素添加修饰性的内容。此元素默认为行内元素。



示例：选中li时，修改背景图片，且添加勾图标（图标由伪元素实现，伪元素要根据父级li进行定位）

```html
    <ul>
        <li>Buy milk</li>
        <li>Take the dog for a walk</li>
        <li>Exercise</li>
        <li>Write code</li>
        <li>Play music</li>
        <li>Relax</li>
    </ul>
    <script>
        var list = document.querySelector('ul');
        list.addEventListener('click', function (ev) {
            if (ev.target.tagName === 'LI') {
                ev.target.classList.toggle('done');
            }
        }, false);
    </script>
```

```css
        li {
            list-style-type: none;
            position: relative;
            margin: 2px;
            padding: 0.5em 0.5em 0.5em 2em;
            background: lightgrey;
            font-family: sans-serif;
        }

        li.done {
            background: #CCFF99;
        }

        li.done::before {
            content: '';
            position: absolute;
            border-color: #009933;
            border-style: solid;
            border-width: 0 0.3em 0.25em 0;
            height: 1em;
            top: 1.3em;
            left: 0.6em;
            margin-top: -1em;
            transform: rotate(45deg);
            width: 0.5em;
        }
```

https://developer.mozilla.org/zh-CN/docs/Web/CSS/::before



#### content属性

CSS的 `content` CSS 属性用于在元素的  [`::before`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/::before) 和 [`::after`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/::after) 伪元素中插入内容。使用`content` 属性插入的内容都是匿名的*[可替换元素](https://developer.mozilla.org/zh-CN/docs/Web/CSS/Replaced_element)。*

> ```
> content: 'prefix' 字符串
> 
> content: " (" attr(id) ")"; attr()方法获取元素的属性值
> 
> content: url(http://www.mozilla.org/favicon.ico) 图片
> 
> 
> ::before   { content: open-quote } 左引号
> ::after    { content: close-quote }右引号
> 
> content: '\1f4a1'; 引入特殊图标；\1f4a1是系统灯泡
> 也可以引入阿里矢量图
> 
> content: "→";
> ```



### 3、::selection  兼容性IE9

**`::selection`** CSS伪元素应用于文档中被用户高亮的部分（比如使用鼠标或其他选择设备选中的部分）。

只有一小部分CSS属性可以用于`::selection` 选择器：

- [`color`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/color)
- [`background-color`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/background-color)
- [`cursor`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/cursor)
- [`caret-color`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/caret-color)
- [`outline`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/outline) and its longhands
- [`text-decoration`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/text-decoration) and its associated properties
- [`text-emphasis-color`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/text-emphasis-color)
- [`text-shadow`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/text-shadow)

注意：系统有自己默认的选中时的样式。

> `::selection` CSS伪元素选择器是CSS第3级选择器的草案，但是在被推荐使用前就被废弃。它现在在第4级伪元素选择器草案中。

**实例：使用的时候，感觉和伪类一样**

```html
    This text has special styles when you highlight it.
    <p>Also try selecting text in this paragraph.</p>
```

```css
        /* 选中的文本是红色背景，金黄色的字体 */
        ::selection {
            color: gold;
            background-color: red;
        }

        /*选中的是蓝色背景，白色的字体的段落*/
        p::selection {
            color: white;
            background-color: blue;
        }
```

**兼容性：IE9，但Firefox的兼容性为62，所以要做兼容性处理，使其兼容早期的Firefox：**

```css
::-moz-selection {
  color: gold;
  background-color: red;
}

p::-moz-selection {
  color: white;
  background-color: blue;
}

/* 选中的文本是红色背景，金黄色的字体 */
::selection {
    color: gold;
    background-color: red;
}

/*选中的是蓝色背景，白色的字体的段落*/
p::selection {
    color: white;
    background-color: blue;
}
```

### 4、::first-line (:first-line)

**`::first-line`** CSS伪元素在某块级元素的第一行应用样式。第一行的长度取决于很多因素，包括元素宽度，文档宽度和文本的文字大小。

 **::first-line 伪元素只能在块容器中，所以，`::first-line伪元素`只能在一个display值为block, `inline-block`, `table-cell` 或者 `table-caption中有用`.。在其他的类型中，`::first-line` 是不起作用的。

在一个使用了 `::first-line 伪元素的选择器中，`只有很小的一部分css属性能被使用：

- 所有和字体有关的属性：[`font`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/font), [`font-kerning`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/font-kerning), [`font-style`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/font-style), [`font-variant`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/font-variant), [`font-variant-numeric`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/font-variant-numeric), [`font-variant-position`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/font-variant-position), [`font-variant-east-asian`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/font-variant-east-asian), [`font-variant-caps`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/font-variant-caps), [`font-variant-alternates`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/font-variant-alternates), [`font-variant-ligatures`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/font-variant-ligatures), [`font-synthesis`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/font-synthesis), [`font-feature-settings`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/font-feature-settings), [`font-language-override`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/font-language-override), [`font-weight`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/font-weight), [`font-size`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/font-size), [`font-size-adjust`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/font-size-adjust), [`font-stretch`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/font-stretch), and [`font-family`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/font-family)
-  [`color`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/color)
- 所有和背景有关的属性： [`background-color`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/background-color), [`background-clip`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/background-clip), [`background-image`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/background-image), [`background-origin`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/background-origin), [`background-position`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/background-position), [`background-repeat`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/background-repeat), [`background-size`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/background-size), [`background-attachment`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/background-attachment), and [`background-blend-mode`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/background-blend-mode)
-  [`word-spacing`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/word-spacing), [`letter-spacing`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/letter-spacing), [`text-decoration`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/text-decoration), [`text-transform`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/text-transform), and [`line-height`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/line-height)
-  [`text-shadow`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/text-shadow), [`text-decoration`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/text-decoration), [`text-decoration-color`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/text-decoration-color), [`text-decoration-line`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/text-decoration-line), [`text-decoration-style`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/text-decoration-style), and [`vertical-align`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/vertical-align).

这个列表将来可能会被扩展，但是推荐的是，你不要使用任何上述没有提到的属性。

`margin-left` 在 first-line 伪元素上无效。

`text-indent` 在 first-line 伪元素上无效。



**语法：**

```css
/* CSS3 syntax */
::first-line

/* CSS2 syntax */
:first-line
```

**兼容性问题：**

> 在CSS 2中，伪元素是以 : 开头的。由于伪类也遵循同一规则，使得他们之间难以区分。——IE5.5
>
> 为了解决这个问题，在CSS 2.1中，伪元素支持以 :: 开头。现在，使用伪元素时更推荐以 :: 开头，而使用伪类时使用 : 开头。
>
> 因为过去的浏览器都实现过CSS 2的规则，所以现在那些支持 :: 的浏览器通常同时也支持 : 的形式。
>
> 如果需要支持老旧的浏览器，那么`:first-line` 是唯一的选择，反之，更推荐使用`::first-line。`



实例：将每个段落中的第一行字母转换成大写

```html
<p>Lorem ipsum dolor sit amet, consectetur adipisicing elit,
sed do eiusmod tempor incididunt ut labore.</p>
```

```css
p::first-line { text-transform: uppercase }
```

### 5、::first-letter (:first-letter)

`::first-letter会`选中某 块级元素第一行的第一个字母，并且文字所处的行之前没有其他内容（如图片和内联的表格） 。

首行只在 [block-container box](https://developer.mozilla.org/en/CSS/Visual_formatting_model#Block-level_elements_and_block_boxes)内部才有意义, 因此 `::first-letter` 伪元素 只在[`display`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/display)属性值为block, `inline-block`, `table-cell`, `list-item` 或者 `table-caption`的元素上才起作用. 其他情况下, `::first-letter` 毫无意义.

只有一小部分CSS可以在包含`使用了::first-letter` 伪元素选择器的CSS规则集声明块内运用:

- 所有的字体属性 : [`font`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/font), [`font-style`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/font-style), [`font-feature-settings`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/font-feature-settings), [`font-kerning`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/font-kerning), [`font-language-override`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/font-language-override), [`font-stretch`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/font-stretch), [`font-synthesis`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/font-synthesis), [`font-variant`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/font-variant), [`font-variant-alternates`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/font-variant-alternates), [`font-variant-caps`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/font-variant-caps), [`font-variant-east-asian`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/font-variant-east-asian), [`font-variant-ligatures`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/font-variant-ligatures), [`font-variant-numeric`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/font-variant-numeric), [`font-variant-position`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/font-variant-position), [`font-weight`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/font-weight), [`font-size`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/font-size), [`font-size-adjust`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/font-size-adjust), [`line-height`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/line-height) 以及 [`font-family`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/font-family).
- 所有的背景属性 : [`background-color`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/background-color), [`background-image`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/background-image), [`background-clip`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/background-clip), [`background-origin`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/background-origin), [`background-position`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/background-position), [`background-repeat`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/background-repeat), [`background-size`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/background-size), [`background-attachment`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/background-attachment)以及 [`background-blend-mode`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/background-blend-mode).
- 所有的外边距属性: [`margin`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/margin), [`margin-top`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/margin-top), [`margin-right`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/margin-right), [`margin-bottom`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/margin-bottom), [`margin-left`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/margin-left).
- 所有的内边距属性: [`padding`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/padding), [`padding-top`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/padding-top), [`padding-right`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/padding-right), [`padding-bottom`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/padding-bottom), [`padding-left`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/padding-left).
- 所有的边框属性: 比如一些简短的边框属性 [`border`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border), [`border-style`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-style), [`border-color`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-color), [`border-width`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-width), [`border-radius`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-radius), [`border-image`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-image), 还剩下许多冗长的边框属性等等.
- [`color`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/color) 属性.
- [`text-decoration`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/text-decoration), [`text-shadow`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/text-shadow), [`text-transform`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/text-transform), [`letter-spacing`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/letter-spacing), [`word-spacing`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/word-spacing) (使用恰当的话), [`line-height`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/line-height), [`text-decoration-color`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/text-decoration-color), [`text-decoration-line`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/text-decoration-line), [`text-decoration-style`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/text-decoration-style), [`box-shadow`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/box-shadow), [`float`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/float), [`vertical-align`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/vertical-align) `注意此刻必须没有浮动`) 等属性.

当这个列表以后被实现时, 为了保持css不过时.建议你不要在声明块内使用任何其他属性.

对于 CSS 2, 伪元素采用单冒号前缀语法. 因为伪类也是同样的语法,所以使得两者难以区分. CSS2.1 改变了伪元素的前缀语法可以解决这个问题. 现在伪元素采用双冒号前缀, 并且伪类仍然采用单冒号前缀.

CSS2伪类单冒号语法已得到广泛支持时, 所有支持双冒号的浏览器同样也支持旧的单冒号语法.

考虑浏览器兼容性的话, `:first-letter` 是一个更有效的选择; 否则, `::first-letter` 更受欢迎.

```css
/* 使每段开头的第一个字母变红变大 */

p::first-letter {  /* 使用:first来兼容IE8- */
  color: red;
  font-size: 130%;
}
```

https://developer.mozilla.org/zh-CN/docs/Web/CSS/::first-letter