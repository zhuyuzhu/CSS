# User-action pseudo classes 用户行为伪类

一些伪类只会在用户以某种方式和文档交互的时候应用。这些**用户行为伪类**，有时叫做**动态伪类**，表现得就像是一个类在用户和元素交互的时候加到了元素上一样。

### 一、LVHA的先后顺序（CSS属性，兼容旧的IE）

为了可以正确地渲染链接元素的样式，防止样式被后声明的其他链接相关的伪类覆盖。

按先后顺序申明：`:link` — `:visited` — `:hover` — `:active`。

**1、:link**

选中尚未访问的链接

```css
a:link {color: slategray;}
```

https://developer.mozilla.org/zh-CN/docs/Web/CSS/:link

**2、:visited**

**`:visited`** CSS[伪类](https://developer.mozilla.org/en-US/docs/CSS/Pseudo-classes)表示用户已访问过的链接。

**出于隐私原因，可以使用此选择器修改的样式非常有限。经过测试谷歌浏览器就不生效。**



**3、:hover**  可以任何伪元素上使用。悬停即触发。

> **注意**: 在触摸屏上 `:hover` 有问题，基本不可用。不同的浏览器上`:hover` 伪类表现不同。 可能从不会触发；或者在触摸某元素后触发了一小会儿；或者总是触发即使用户不在触摸了，直到用户触摸别的元素。 触摸屏非常普遍，所以网页开发人员不要让任何内容只能通过悬停才能展示出来，不然这些内容对于触摸屏使用者来说是很难或者说不可能看到。

https://developer.mozilla.org/zh-CN/docs/Web/CSS/:hover

**4、:active** [伪类](https://developer.mozilla.org/zh-CN/docs/CSS/Pseudo-classes)匹配被用户激活的元素。它让页面能在浏览器监测到激活时给出反馈。**当用鼠标交互时，它代表的是用户按下按键和松开按键之间的时间**。`:active` 伪类一般被用在  **a** 和 **button**元素中。这个伪类的一些其他适用对象包括包含激活元素的元素，以及可以通过他们关联的**label**标签被激活的表格元素。

**也可以用在其他标签上**。

https://developer.mozilla.org/zh-CN/docs/Web/CSS/:active

#### LVHA示例：

```html
    <p>This paragraph contains a link:
        <a href="#">This link will turn red while you click on it.</a>
        The paragraph will get a gray background while you click on it or the link.
    </p>
```

```css
        a:link { color: blue; }          /* 未访问链接 */
        a:visited { color: purple; }     /* 已访问链接 */
        a:hover { background: yellow; }  /* 用户鼠标悬停 */
        a:active { color: red; }         /* 激活链接 */

        p:active { background: #eee; }   /* 激活段落 */

```

### 二、其他

**1、:target  兼容性IE9**



https://developer.mozilla.org/zh-CN/docs/Web/CSS/:invalid

**`:target`** 

**`:target`** [CSS](https://developer.mozilla.org/en-US/docs/Web/CSS) [伪类](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-classes) 代表一个唯一的页面元素(目标元素)，其`id` 与当前URL片段匹配 .

元素的id值与url的hash值对应时，:target目标元素，就是指URL的hash值所指的元素id。

示例：

```html
    <h3>Table of Contents</h3>
    <ol>
        <li><a href="#p1">Jump to the first paragraph!</a></li>
        <li><a href="#p2">Jump to the second paragraph!</a></li>
        <li><a href="#nowhere">This link goes nowhere,
                because the target doesn't exist.</a></li>
    </ol>

    <h3>My Fun Article</h3>
    <p id="p1">You can target <i>this paragraph</i> using a
        URL fragment. Click on the link above to try out!</p>
    <p id="p2">This is <i>another paragraph</i>, also accessible
        from the links above. Isn't that delightful?</p>
```

点击a标签时，a标签的锚点作用，给url添加hash值，hash值对应p标签的id。因此`p:target`的伪类生效。

如果不用a标签来改变hash值，直接修改url的hash值，使与p标签的id值对应，同样会使`p:target`的伪类生效。

https://developer.mozilla.org/zh-CN/docs/Web/CSS/:target

**2、元素required属性和伪类:required  兼容性IE10**

（1）元素required属性 ——提交表单前必填项  兼容性IE10

HTML5 中的新属性，required 属性是一个布尔属性。**required 属性规定在提交表单之前必需填写输入字段。**

**注意：**required 属性适用于下面的 input 类型：text、search、url、tel、email、password、date pickers、number、checkbox、radio 和 file。

（2）伪类:required  匹配必填项    兼容性IE10

示例：

```html
    <form action="demo-form.php">
        Username: <input type="text" name="usrname" required>
        <input type="submit">
    </form>
```

```css
input:required {
  background-color: #800000;
  border-width: 3px;
}
```

**3、:valid  和  :invalid**   兼容性 IE10

`:valid`匹配填了有效值的元素。

表示内容[验证](https://developer.mozilla.org/en/HTML/HTML5/Constraint_validation)正确的input或其他form元素。这能简单地将校验字段展示为一种能让用户辨别出其输入数据的正确性的样式。

**`:invalid`**

 表示任意内容未通过验证的 input 或其他 form元素 .

`:invalid`这个伪类对于突出显示用户的字段错误非常有用。

根据 input的类型，比如type="url" 、type="email"，进行检测，如果输入的内容跟input要求的类型不一样，将触发**`:invalid`**伪类。

示例：

```html
    <form action="demo-form.php">
        Username: <input type="text" name="usrname" required>
        <input type="submit">
    </form>
```

```css
/* 无效值的input元素 */
input:invalid {
  background-color: #ffdddd;
}
/* 无效值的form元素 */
form:invalid {
  border: 5px solid #ffdddd;
}
/* 有效值的input元素 */
input:valid {
  background-color: #ddffdd;
}
/* 有效值的form元素 */
form:valid {
  border: 5px solid #ddffdd;
}
/* 必填值的input */
input:required {
  border-color: #800000;
  border-width: 3px;
}
/* 必填值且无效值的input元素 */
input:required:invalid {
  border-color: #C00000;
}
```

注意：form表单内的input输入框有效、无效会使得该form表单有效、无效。



**4、:indeterminate ** 兼容性：IE10

表示状态不确定的表单元素。

https://developer.mozilla.org/zh-CN/docs/Web/CSS/:indeterminate

根据上述例子（选择器）选中的元素是：

- `<input type="checkbox">` 元素，其 `indeterminate` 属性被 [JavaScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript)设置为 `true` 。
- `<input type="radio">` 元素, 表单中拥有相同 `name`值的所有单选按钮都未被选中时。
- 处于不确定状态的 progress元素

实例：

```html
    <div>
        <input type="checkbox" id="checkbox">
        <label for="checkbox">Background should be green</label>
    </div>
    <div>
        <input type="radio" name="ra" id="radio1" class="rad">1
        <input type="radio" name="ra" id="radio2" class="rad">2
        <input type="radio" name="ra" id="radio3" class="rad">3
    </div>
```

```css
        #checkbox:indeterminate {
            width: 20px;
            height: 20px;
        }

        input[name=ra]:indeterminate {
            width: 20px;
            height: 20px;
        }
```

```js
        var input = document.getElementsByTagName("input")[0];
        input.indeterminate = true;
```

注意：

复选框input必须通过js设置indeterminate属性。

单选框，相同name值的所有单选框都未选中时，处于indeterminate状态。**注意：**IE浏览器:indeterminate伪类无法修饰未确定状态下的单选框。



### 三、补充知识

1、progress元素   兼容性IE10

```html
   <progress max="100" value="70"></progress>
```

可以通过操作progress元素的value值，动态修改进度条。

该属性用来指定该进度条已完成的工作量.如果没有`value属性`,则该进度条的进度为"不确定",也就是说,进度条不会显示任何进度,你无法估计当前的工作会在何时完成(比如在下载一个未知大小的文件时,下载对话框中的进度条就是这样的)

没有value值时，progress元素处于未确定状态，此时的`progress:indeterminate`伪类可以匹配到该元素。注意value=0时，也是有value值，不处于未确定状态。

未确定状态：

```html
<progress max="100"></progress>
```

不同浏览器的默认浏览器样式（user agent sheetstyle）不一样。动画样式不同。

<progress max="100"></progress>

谷歌浏览器的默认样式：

```css
    -webkit-writing-mode: horizontal-tb !important;
    appearance: progress-bar;
    box-sizing: border-box;
    display: inline-block;
    height: 1em;
    width: 10em;
    vertical-align: -0.2em;
```



如果通过伪类:indeterminate修改background-color，来修饰进度条，结果：

Chrome：失去动画效果，当做一个inline-block，进行样式渲染。

IE：没有失去动画效果，:indeterminate新增的样式，将作用到progress上。

Firefox：没有失去动画效果，background-color被修改后，总是为蓝色。

如果修改别的属性，不会失去动画效果，比如：width、height、