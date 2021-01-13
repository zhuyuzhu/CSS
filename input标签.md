https://developer.mozilla.org/zh-cn/docs/web/html/element/input

# input标签

**HTML `<input>` 元素**用于为基于Web的表单创建交互式控件，以便接受来自用户的数据; 可以使用各种类型的输入数据和控件小部件，具体取决于设备和[user agent](https://developer.mozilla.org/zh-CN/docs/Glossary/User_agent)。

#### input属性

`<input>`元素由于拥有诸多属性而异常强大，其中前文举例说明的`type`属性尤其重要。由于所有`<input>`元素，无论是哪种 `type` ，都基于[`HTMLInputElement`](https://developer.mozilla.org/zh-CN/docs/Web/API/HTMLInputElement)接口，所以理论上说，它们共享一套相同的属性。但实际上大部分属性只作用于特定一组 `type`。此外，一些属性作用于`<input>`的方式取决于`<input>`的`type`属性，不同的`type`有不同的效果。

input元素的属性包括[全局HTML属性](https://wiki.developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes)和以下属性：



#### input标签的类型

<input>的工作方式根据其type属性的值有很大的不同，因此不同的类型在各自单独的参考页面中进行了介绍。如果未指定此属性，则采用的默认类型为text。

button类型：

一个没有默认行为的按钮，按钮上显示value属性的值，默认情况value为空，页面按钮上没有内容。

```html
<input type="button" value="按钮">
```

button类型的元素被渲染为简单的按钮，当指定一个事件处理函数(通常用于单击事件)时，可以编程来控制网页上任何需要的自定义功能。

虽然button类型的<input>元素仍然是完全有效的HTML，但<button>元素现在是创建按钮的首选方式。

<input type="button">元素没有默认行为(它们的表兄弟<input type="submit">和<input type="reset">分别用于提交和重置表单)。要让按钮做任何事情，您必须编写JavaScript代码来完成这项工作。

给按钮添加键盘快捷键：

https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/button#adding_keyboard_shortcuts_to_buttons

https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes#attr-accesskey

键盘快捷键，也称为访问键和键盘等效键，允许用户使用键盘上的一个键或多个键组合来触发按钮。要向按钮添加一个键盘快捷方式——就像使用任何有意义的<input>一样——需要使用accesskey全局属性。