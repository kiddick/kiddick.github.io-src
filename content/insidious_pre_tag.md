Title: Insidious &#8826;pre&#8827; tag
Date: 2015-12-23
Category: Web design
Tags: HTML, CSS

I have faced with strange behavior in inheritance of attributes in CSS. Since I've added `pygments.css` with syntax highlighting everything was ok apart from default font in block with highlighting of syntax.

There is several classes and several nested tags:

```html
<div class="parent">
  <pre>
    <div class="another">
      inner-pre-div
    </div>
  </pre>
   <div class="another">
     inner-div
   </div>
</div>
```

and some styling for that:

```css
.parent {
  font-size: 25px;
  font-family: cursive;
}

.another {
  font-size: 35px;
}

body {
  font-family: Courier;
}
```

For some reason text in `div` nested to `pre` hasn't inherited `font-family` attribute from `parent` class. Although `div` nested to another `div` has worked correctly.

The reason for this is the specific of `pre` tag.
There are next default values for that:

```css
pre {
    display: block;
    font-family: monospace;
    white-space: pre;
    margin: 1em 0;
}
```

So it overrides `font-family` by default.
That's why we were unable to change it in `another` class.

We need explicitly override `font-family` for `pre` tag:

```
.parent pre {
  font-family: cursive;
}
```

There is [jsfiddle](https://jsfiddle.net/029rz40w/) with examined example.
