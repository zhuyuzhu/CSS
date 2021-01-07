## CSS中的特殊符号

**1、通配符 ***

```css
        * {
            margin: 0px;
            padding: 0px;
            list-style: none;
        }
```



**2、后面兄弟元素 ~**

```css
        div ~ p {
            color: #f40;
        }
```

```html
    <p>22</p>
    <div>
        <p>33</p>
    </div>
    <p>44</p>
    <p>55</p>
```

44、55是淘宝红。

**3、后面紧跟着的兄弟元素 +**

```css
        div + p {
            color: #f40;
        }
```

```html
    <p>22</p>
    <div>
        <p>33</p>
        <ul>
            <p>55</p>
        </ul>
    </div>
    <p>44</p>
```

只有44是淘宝红。

**解读：**div后面的第一个兄弟元素必须是p。选中该p元素。

**4、直接子元素 >**

```css
        div > p {
            color: #f40;
        }
```

```html
    <p>22</p>
    <div>
        <p>33</p>
        <ul>
            <p>55</p>
        </ul>
    </div>
    <p>44</p>
```

只有33是淘宝红。

