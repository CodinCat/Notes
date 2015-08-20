##平分填滿子元素高

在`.fill-height`已有一個高度的情況下：

```html
<div class="fill-height">
    <div></div>
    <div></div>
    <div></div>
</div>
```

```css
.fill-height {
    display: flex;
    flex-direction: column;
}
.fill-height > div {
    flex: 1;
    justify-content: center;
    flex-direction: column;
}
```

```
flex: 1;

等於
flex: 1 1 auto;

等於
flex-grow: 1;
flex-shrink: 1;
flex-basis: auto;
```

##填滿剩餘高度

同樣`.box`已有一個高度時，以下範例header及footer的高度根據自己的內容而定，而`.box`所剩餘的空間將會由中間的`div`自動補滿：
```html
<div class="box">
    <header class="flex-auto">Hello</header>
    <div class="flex-fill">自動補滿高度</div>
    <footer class="flex-auto">World</footer>
</div>
```

```css
.box {
    display: flex;
    flex-direction: column;
}
.flex-auto {
    flex: 0 1 auto;
}
.flex-fill {
    flex: 1 1 auto;
}
```
