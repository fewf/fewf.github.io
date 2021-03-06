---
layout: post
title: Blog Changes and Border Image (and Utz chips)
---

I've got a new URL, at least temporarily. Free hosting on Github is neat, and easy to set-up thanks to [jekyll-now](https://github.com/barryclark/jekyll-now). By default, it gives you a very basic look to your blog. But, of course, I wanted to keep my Utz-inspired theme which I'd built in Wordpress.

![Utz's brilliant style]({{ site.url }}/images/utz.jpg)

Warning: It's going to get a bit nerdy from here.

The old way that I achieved this effect was by a real ugly hack. It relied on a three-column div layout--so that the blue border you see to the left and right were actual block elements, with the background color set, and with either the top-right or top-left corner set to have a border-radius.

Now, this is bad for many reasons, but perhaps most because it violates the intended purpose of HTML: to provide a semantic structure to content. Kind of like declaring "This is the header, this is the main portion, this is a blog post within the main portion, this is the footer, etc". HTML's friend CSS comes in to provide the style to all those elements.

The Jekyll-now default HTML is a perfect example of this, encapsulating the simple structure of a blog. So, I decided my goal was to achieve my Utz styling without altering the hypertext, just the CSS. Et voila, that's what we have here.

I realized that what I essentially wanted was a custom border to the "main" section of the page (i.e., the one holding the text you're reading now). Enough queries Google eventually led me to find [the border-image property](https://developer.mozilla.org/en-US/docs/Web/CSS/border-image). It's a tremendously powerful alternative to the typical border CSS you might know and love. I'll try my best to explain.

Here is the actual source image of the border that you see around this text right now.

![the actual border you're looking at now]({{ site.url }}/images/utz-border-image.svg)

It's an SVG which the browser is slicing up into a 3x3 grid. The CSS looks like this:

```
#main {
    border-image-source: url(.../utz-border-image.svg);
    border-image-slice: 32 64 39;
    border-image-repeat: stretch;
    border-width: 4em 7em;	
}
```

It gives the browser the image and says slice it thiswise:

* One horizontal slice 32 pixels from the top.
* One horizontal slice 39 pixels from the bottom.
* Two vertical slices, one 64 pixels in from the right, the other 64 pixels in from the left.

For a final product that would look thusly:

![sliced and zoomed]({{ site.url }}/images/utz-border-image-sliced.svg)

We now have our 3x3 grid. Let's use directions to refer to the gridded off chunks; we've got a N S E and W chunks, as well as NW, NE, SE and SW chunks. Lastly, the very center of this grid is the thing to be bordered (once again, the text you're reading now).

Now, with this information, the browser knows to stretch what it finds in the E and W chunks as the bordered content grows in height, and likewise to use what's in N and S to stretch for the width. (If `border-image-repeat` is set to `repeat`, it will repeat instead of stretch. For this usage, the effect is identical.) The imagery inside the NW, NE, SE and SW chunks will sit unaffected by the length or width of the content at the corners of the borders. What does affect those corners is the `border-width`, which tells the browser to stretch it so that the width is 4em and height is 7em.

Hope this makes sense--and keep snacking!
