##Flex平分填滿子元素高

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
