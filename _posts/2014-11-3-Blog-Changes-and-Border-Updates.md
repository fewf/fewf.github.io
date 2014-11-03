---
layout: post
title: Blog Changes and Border Image (and Utz chips)
---

I've got a new URL, at least temporarily. Free hosting on Github is neat, and easy to set-up thanks to [jekyll-now](https://github.com/barryclark/jekyll-now). As a default, you'll get a very basic look to your blog. But, of course, I wanted to keep my Utz-inspired theme which I'd built in Wordpress.

![Utz's brilliant style](../images/utz.jpg)

The way that I achieved this effect in the old Wordpress was a bit of a hack. It relied on a pre-built three-column div layout and border-radius CSS to produce the curved effect. It bloated the mark-up needlessly, making it confusing to maintain. Worse perhaps, it rendered in unpredictable ways when on a narrow screen. Moving to this new blog platform, I wanted to take another crack at a more elegant solution. 

I realized that what I essentially wanted was a custom border to the "main" section of the page (i.e., the one holding the text you're reading now). Enough queries Google eventually led me to find [the border-image property](https://developer.mozilla.org/en-US/docs/Web/CSS/border-image). It's a tremendously powerful alternative to the typical border css you might know and love. I'll try my best to explain.

![the actual border you're looking at now](../images/utz-border-image.svg)

This above is the actual border that you see around this text right now. It's an SVG which the browser is slicing up into a 3x3 grid. The CSS looks like this:

>border-image-source: url(http://fewf.github.io/images/utz-border-image.svg);
>border-image-slice: 32 64 39;
>border-image-width: initial;
>border-image-outset: initial;
>border-image-repeat: stretch;