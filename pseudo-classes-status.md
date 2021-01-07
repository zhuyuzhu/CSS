## 伪类（pseudo-classes）状态

#### 状态伪类 

所有的伪类以同样的方式实现。它们选中你的文档中处于某种状态的那部分，表现得就像是你已经向你的HTML加入类一样。(某种状态 ——  某种类样式)

示例：让 一篇文章中第一段字体变大加粗

```css
article p:first-child {
    font-size: 120%;
    font-weight: bold;
}   
```

```html
<article>
    <p>Veggies es bonus vobis, proinde vos postulo essum magis kohlrabi welsh onion daikon amaranth tatsoi tomatillo
            melon azuki bean garlic.</p>

    <p>Gumbo beet greens corn soko endive gumbo gourd. Parsley shallot courgette tatsoi pea sprouts fava bean collard
            greens dandelion okra wakame tomato. Dandelion cucumber earthnut pea peanut soko zucchini.</p>
</article>
```

### 一、根据元素的位置匹配

**1、`:first-child`**：所修饰的元素是其父元素的第一个子元素

**注释：**对于 IE8 及更早版本的浏览器中的 :first-child，必须声明HTML <!DOCTYPE> 标签。

**兼容性：**兼容IE8

使用如下：

（1）示例中，没有一个p元素符合，是其父级元素的第一个child元素。

```css
    div p:first-child {
        color: hotpink;
    }
```

```html
    <div>
        <div>
            <a href="">1212</a>
            <p>333</p>
        </div>
        <p>4444</p>
        <span>111</span>
        <p>22222</p>
    </div>
```

（2）示例：div标签下的第一个child元素为p元素，该p元素下的i标签

```css
        div p:first-child i{
            color: hotpink;
        }
```

```html
    <div>
        <p>
            <i>111</i>
            <i>222</i>
        </p>
    </div>
```

（3）示例：p标签是其父级元素下的第一个child元素，都被添加下面的样式

```css
        p:first-child{
            color: hotpink;
        }
```

**2、`:last-child`**：修饰元素是其父元素的最后一个子元素

兼容性IE9

**3、`:first-of-type`**  表示一组兄弟元素中其类型的第一个元素。

兼容性：IE9

示例：div下所有的p标签中，第一个p标签，添加下面样式

```css
div p:first-of-type {
  		color: red;
 	 	font-style: italic;
}
```

```html
<div>
    <h2>Heading</h2>
	<p>Paragraph 1</p>
	<p>Paragraph 1</p>
</div>
```

**4、`:last-of-type`**：表示了在（它父元素的）子元素列表中，给定类型的最后一个元素。

兼容性IE9

示例：

```css
p em:last-of-type {
  color: lime;
}
```

```html
<p>
  <em>我没有颜色 :(</em><br>
  <strong>我没有颜色 :(</strong><br>
  <em>我有颜色 :D</em><br>
  <strong>我也没有颜色 :(</strong><br>
</p>

<p>
  <em>我没有颜色 :(</em><br>
  <span><em>我有颜色!</em></span><br>
  <strong>我没有颜色 :(</strong><br>
  <em>我有颜色 :D</em><br>
  <span>
    <em>我在子元素里，但没有颜色!</em><br>
    <span style="text-decoration:line-through;"> 我没有颜色 </span><br>
    <em>我却有颜色！</em><br>
  </span><br>
  <strong>我也没有颜色 :(</strong>
</p>
```

**`5、:nth-child(an+b)`** 首先找到所有当前元素的兄弟元素，然后按照位置先后顺序从1开始排序，选择的结果为CSS伪类:nth-child括号中表达式（an+b）匹配到的元素集合（n=0，1，2，3...）。

兼容性 ：IE9

示例：

- `0n+3` 或简单的 `3` 匹配第三个元素。
- `1n+0` 或简单的 `n` 匹配每个元素。（兼容性提醒：在 Android 浏览器 4.3 以下的版本 `n` 和 `1n` 的匹配方式不一致。`1n` 和 `1n+0` 是一致的，可根据喜好任选其一来使用。）
- `2n+0` 或简单的 `2n` 匹配位置为 2、4、6、8...的元素（n=0时，2n+0=0，第0个元素不存在，因为是从1开始排序)。你可以使用关键字 **`even`** 来替换此表达式。
- `2n+1` 匹配位置为 1、3、5、7...的元素。你可以使用关键字 **`odd`** 来替换此表达式。
- `3n+4` 匹配位置为 4、7、10、13...的元素。

`*a*` 和 `*b*` 都必须为整数，并且元素的第一个子元素的下标为 1。换言之就是，该伪类匹配所有下标在集合 { an + b; n = 0, 1, 2, ...} 中的子元素。另外需要特别注意的是，`*an*` 必须写在 `*b*` 的前面，不能写成 `*b+an*` 的形式。

示例：

（1）表示HTML表格中的奇数行。

```
tr:nth-child(2n+1)
```

（2）表示HTML表格中的偶数行。

```
tr:nth-child(2n)
```

（3）表示HTML表格中的奇数行。

```
tr:nth-child(odd)
```

（4）表示HTML表格中的偶数行。

```
tr:nth-child(even)
```

（5）表示子元素中第一个且为span的元素，与 [`:first-child`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:first-child) 选择器作用相同。

```
span:nth-child(0n+1)
```

（6）表示父元素中子元素为第一的并且名字为span的标签被选中

```
span:nth-child(1)
```

（7）匹配前三个子元素中的span元素。

```
span:nth-child(-n+3)
```



6、**`:nth-of-type()`**：针对具有一组兄弟节点的标签, 用 n 来筛选出在一组兄弟节点的位置。

兼容性 IE9

7、**`:nth-last-of-type(an+b)`** 匹配那些在它之后有 `*a*n+*b*-1` 个相同类型兄弟节点的元素，其中 `n` 为正值或零值。它基本上和 [`:nth-of-type`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:nth-of-type) 一样，只是它从**结尾**处反序计数，而不是从开头处。

兼容性IE9

### 二、根据元素的状态

**1、:disabled   匹配任何被禁用的元素   兼容性IE9**

`:disabled` 匹配任何被禁用的元素。如果一个元素不能被激活（如选择、点击或接受文本输入）或获取焦点，则该元素处于被禁用状态。

元素还有一个启用状态（enabled state），在启用状态下，元素可以被激活或获取焦点。

```css
/* Selects any disabled <input> */
input:disabled {
  background: #ccc;
}
```

**标签的disabled属性：兼容性IE6**

```html
<p>Last name: <input type="text" name="lname" disabled="disabled" /></p>
<p>Last name: <input type="text" name="lname" disabled /></p>
```

https://developer.mozilla.org/zh-CN/docs/Web/CSS/:disabled



**2、:enabled  匹配被启用的元素** 

**`:enabled`** 表示任何被启用的（enabled）元素。如果一个元素能够被激活（如选择、点击或接受文本输入），或者能够获取焦点，则该元素是启用的。元素也有一个禁用的状态（disabled state），在被禁用时，元素不能被激活或获取焦点。

```css
/* 选择任何启用状态的 <input> */
input:enabled {
  color: blue;
}
```

https://developer.mozilla.org/zh-CN/docs/Web/CSS/:enabled

**3、:checked 匹配选中状态的元素**

**`:checked`** CSS [伪类](https://developer.mozilla.org/en-US/docs/CSS/Pseudo-classes)选择器表示任何处于选中状态的**radio**(`<input type="radio">`), **checkbox** (`<input type="checkbox">`) 或("select") 元素中的**option** HTML元素("option")。

```css
/* 匹配任意被勾选/选中的radio(单选按钮),checkbox(复选框),或者option(select中的一项) */
:checked {
  margin-left: 25px;
  border: 1px solid blue;
} 
```

用户通过勾选/选中元素或取消勾选/取消选中，来改变该元素的 :checked 状态。

> 用户通过勾选/选中元素或取消勾选/取消选中，来改变该元素的 :checked 状态。

妙用：纯CSS实现点击隐藏和显示——label代替input实现按钮

```html
    <input type="checkbox" id="expand-toggle" />
    <label for="expand-toggle" id="expand-btn">Toggle hidden</label>

    <div>
        <p>111</p>
        <p>222</p>
        <p>333</p>
    </div>
```

```css
/* input框隐藏 */
#expand-toggle {
  display: none;
}
/* label模拟按钮且触发input的checked属性 */
#expand-btn {
  display: inline-block;
  margin-top: 12px;
  padding: 5px 11px;
  border: 1px solid;
  border-radius: 3px;
  cursor:pointer;
}
/* div下的p标签隐藏 */
div p {
    display: none;
}
/* input checked状态下的后面的兄弟元素div下的p标签 显示 */
#input:checked ~ div p{
  display: block;
}
```

可以实现选项卡：

```html
    <div class="itemRadio">
        <input type="radio" name="test" id="toggle1" checked/>
        <p>111</p>
        <input type="radio" name="test" id="toggle2" />
        <p>222</p>
        <input type="radio" name="test" id="toggle3" />
        <p>333</p>
    </div>
    <div class="content">
    </div>
```

```css
        .itemRadio {
            width: 111px;
            height: 40px;
            border: 1px solid black;

        }
        .itemRadio input {
            position: relative;
            display: inline-block;
            margin-left: 17px;
            margin-top: 10px;
            font-size: 20px;
            cursor: pointer;
        }
        .content {
            width: 111px;
            height: 100px;
            border: 1px solid black;
        }
        p {
            display: none;
            position: absolute;
            top: 50px;
            left: 50px;
        }
        input:checked + p{
            display: block;
        }
```

**特点：input只能操作兄弟元素，以及兄弟元素内的元素。**

具体的实例可以去查看

https://developer.mozilla.org/zh-CN/docs/Web/CSS/:checked

### 三、其他

**1、:not 除了指定元素**

**`:not()`** 用来匹配不符合一组选择器的元素。由于它的作用是防止特定的元素被选中，它也被称为*反选伪类*（*negation pseudo-class*）

```css
    p:not(.num) {
        color: red;
    }
```

```html
    <p>This paragraph contains a link:
        <a id="elementa" href="#">This link will turn red while you click on it.</a>
        <p class="num">111</p>
    </p>
```

p元素中，除了类是num的，被修饰。



- `:not()` 伪类不能被嵌套，这意味着 `:not(:not(...))` 是无效的。
- 由于伪元素不是简单的选择器，他们不能被当作 `:not()` 中的参数，形如 `:not(p::before)` 这样的选择器将不会工作。
- 可以利用这个伪类写一个完全没有用处的选择器。例如， `:not(*)` 匹配任何非元素的元素，因此，这个规则将永远不会被应用。
- 可以利用这个伪类提高规则的[优先级](https://developer.mozilla.org/zh-CN/docs/Web/CSS/Specificity)。例如， `#foo:not(#bar)` 和 `#foo` 会匹配相同的元素，但是前者的优先级更高。
- `:not(.foo)` 将匹配任何非 `.foo` 的元素，*包括 [``](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/html) 和 [``](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/body)*。
- 这个选择器只会应用在一个元素上，无法用它来排除所有父元素。比如， `body :not(table) a` 依旧会应用到表格元素 [``](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/table) 内部的 [``](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/a) 上, 因为 将会被 `:not(table)` 这部分选择器匹配。