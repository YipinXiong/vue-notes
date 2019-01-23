# Rebuild Chinese Uber-eats

## Small tools - Webpack & eslint

`webpack`: convert your code into directly executable code by browser

> webpack.base.conf.js to configure rules.



`eslint`: es6 code style examiner which can desperately uniform the code style of the group by a configure file.  

> in the `.eslintrc.js` file to configure the rules!



## Introduction to `MVVM`

[Nice article introducing MVVM and MVC](https://hackernoon.com/mvc-vs-mvvm-how-a-website-communicates-with-its-data-models-18553877bf7d)

![1547975659540](imgs/1547975659540.png)

![1547982350965](imgs/1547982350965.png)

## What is scaffolder? 

Scaffolder provides developer some primitive codes or fold structures, so that developers don't have to write some trivial code from scratch. `<template-name>` in `vue-cli` indicates what kinds of structures you want to have.



> You can mock data by `webpack`. Find the entry js file and then change the node file. 



## CSS Sticky footers

The purpose of a sticky footer is that it "sticks" to the bottom of the browser window. But not always, if there is enough content on the page to push the footer lower, it still does that. But if the content on the page is short, a sticky footer will still hang to the bottom of the browser window.

[Sticky Footer, Five Ways from css-tricks.com](https://css-tricks.com/couple-takes-sticky-footer/)



## Tips Repository

### Conventions When Writing CSS

- Structure and position attributes first; then style attributes

### `line-height` vs `height`

If the content overflows one line in a `div`, the line-height will display two lines whose height is the value of `line-height`. While `height` only sets the `div` to single line, displaying the box-height as the value of `height` 

### display: block

use this on styling `<a>`, which will make the whole outside container tag clickable



###  repaint vs reflow

[What are repaint and reflow?](http://www.cnblogs.com/cencenyue/p/7646718.html)



### @media & media queries

[MDN: what is media query and why we need it? How do we use it?](https://developer.mozilla.org/en-US/docs/Web/CSS/Media_Queries/Using_media_queries)

You need media query to identify the `dpr` of the device, which will determine which icon file will be applied.

```stylus
bg-image($url)
	background-image: url($url + "@2x.png")
	@media (-webkit-min-device-pixel-ratio: 3), (min-device-pixel-ratio: 3)
    background-image: url($url + "@3x.png")
```

> To display a image, you don't have to use `<img>` but `<span>` then set `inline-block` and background.

### `vertical-align`

This is a self-explanatory property in CSS. If you notice that some sibling tags are not aligned well, you can use this property. 

`vertical-align: top` (align by wrapper)



### Hide the content overflow one line

We sometimes wanna hide the content overflowing the line and display "..." to prompt that there is hidden content. To achieve this:

```css
white-space: nowrap
overflow: hidden
text-overflow: ellipsis
```

> Sequences of whitespace will collapse into a single whitespace. Text will never wrap to the next line.



### position fixed vs absolute

`fixed` is really fixed, while the content will change according to the movement of scrollbar in `absolute` mode. 

 

### Why we need `font-size: 0` in `inline-block`?

[Chinese Explanation with pics](https://segmentfault.com/q/1010000008628181)



### Best case for table layout

When you need some grids to display the content with several lines and text should be placed in the center, you should consider `display: table-cell`