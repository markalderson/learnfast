# Learn CSS in 10 minutes

CSS (Cascading Style Sheets) _really_ is a simple technology that you can learn in minutes.
Like all web technologies it has its own history and is continously evolving, but the main concepts
you need to know to understand how it works are just a few, they're quite stable and really simple.

**Note:** This tutorial assumes basic HTML knowledge.

## Selectors and rules

Old web sites used to express both page _structure_ and page _style_ via HTML. For instance, HTML
was used not only to express that a particular string is a heading, but also to tell how that
heading has to be styled (e.g. its size, color, alignment, etc.).

Nowadays, a page style is often described in CSS language, mostly through separated files
referenced from HTML via `<link>` tags inside the `<head>` tag:

``` html
<link href="my_style.css" rel="stylesheet">
```

This is good for web developers, since they can now develop structure and style more independently and,
thus, write more mantainable code. But it's also good for HTML itself, as a standard web technology:
its purpose is now more focused and its evolution may become easier.

Clearly, CSS code needs a means to reference content inside HTML and apply style to it. This is
CSS _selctors_' job. A selector is a character sequence used to identify a subset of an HTML
document. We'll see how CSS selectors work in a while.

Once you can select portions of page content, you need a way to style them, and this is what CSS _rules_ do.
A rule applies to a _property_ and assigns a value to it. Each property controls a styling aspect. For example,
the `color` property applies a specific color to text.

So, basically CSS is a collection of declarations, each one composed of a selector and a set of rules
that will apply to the content _matching_ the selector.

## Writing selectors

The simplest form of selector is a string corresponding to an HTML tag name. These selectors select all the
elements with that tag name. So, for example, this:

``` css
p { font-size: 12px; }
```

will apply a 12px font size for all the `p` elements inside the HTML document.

A common pattern when working with CSS is to select elements based on their `id` or `class` attribute, because
CSS has dedicated syntax: if you have an element with `id="foo"`, you can select it with `#foo`; if you have an
element with `class="foo"`, you can select it with `.foo`.

**Note:** `id` values should be unique within a page. Conversely, the same `class` value may be applied to
multiple elements. Also, the same element may have multiple classes, you just comma-separate them inside
the `class` attribute's value declaration (e.g. `class="foo bar"` applies both class `foo` and class `bar`).

Selectors may be combined. For example if `s1` and `s2` are two valid CSS selectors:

* `s1 s2` selects all the elements matching `s2` and are _descendants_ of elements matching `s1`
* `s1 > s2` selects all the elements matching `s2` and are _children_ of elements matching `s1`
* `s1, s2` selects all the elements matching `s1` or `s2`

So, for instance, `#content h1 > .first_word` selects all the elements with `class="first_word"` children of
`h1` elements inside the element with `id="content"`. As you can see from this example, with just a few basic rules
and with smart usage of `id` and `class` attributes, you are ready to write very specific selectors.

More on CSS selectors [here](http://www.w3schools.com/cssref/css_selectors.asp).

## Writing rules

Rules follow this syntax:

```
<property>: <value>;
```

Rules immadiately follow the associated selector and are enclosed in braces.

Commonly used proprties are:

* `display` to control whether the element should be displayed and if it should be laid out on its own line or not
* `width`, `height`, `max-width`, `max-height`, `min-width` to deal with the element's size
* `margin`, `border` and `padding` to manage spacing around the element
* `background` to set a color or a picture as background for the element
* `color`, `font-family`, `font-size`, `font-weight`, `font-style`, `text-decoration` to style text

There are too much properties to document each on of them. You should think about what styling problem
do you have and then search on google: eventually, you'll find the property you were searching for.

Property values are even wilder: some have units (e.g. `10px`), some have special syntax (e.g. `#000000` is a way
to denote the color black). In general, each property has its own rules for values, although some rules are
sometimes shared by multiple properties. You should refer to the
[official specifications](http://www.w3.org/standards/techs/css#w3c_all) (that may be hard to read, though) or
to some good, updated documentation resources like [this one](http://www.w3schools.com/css/).

## Layouts

Styling a page surely means taking care of stuff like background color, font size, etc. But perhaps the most
important style-related concern is layout. People use CSS to tell the browser how the elements in their
HTML documents should be laid out.

Sadly, CSS layouts are complex stuff. You want some pieces of your page to be centered and others to align on one side.
Maybe some portions of your page should always be visible (e.g. a navigation bar) and others can be hidden
when scrolling. Some should have very specific size, otherwise your design will be broken.
Well, these reasonable constraints are difficult so satisfy with CSS.
You'll see that most of the time it feels like the language is missing appropriate properties for
layout problems and that existing proprerties somitime work in surprising ways, leaving you with the idea that instead
of really solving a problem you just found a trick. Often, these tricks works just for some browsers.
It's also sadly common that styling problems force you to clutter your HTML structure with useless
elements required for some styling trick.

That said, it's also true that you can design a lot of decent and robust layouts with proper use of the `margin`
property. So we can say that, while waiting for better layout support, we can go and lean all the cool-yet-odd
tricks. Or we can stick to a limited toolset of regular techniques.

## Media queries

CSS3 allows you to apply rules based on device properties such as width, height and orientation. This makes possible
to realize _responsive designs_, i.e. layouts that work for different devices and device orientations.

Look at this example of how to hide a sidebar _only_ on small devices:

``` css
@media (max-width: 600px) {
  #sidebar {
    display: none;
  }
}
```

More on media queries [here](https://developer.mozilla.org/en-US/docs/Web/Guide/CSS/Media_queries).

## Animations

The web is full of web sites with cool special effects, and it was like this since _Flash_ was invented many years ago.
Being proprietary software, Flash is not a good match for web technologies. The _W3C_ (World Wide Web Consortium) is working
hard to replace Flash with open alternatives, based on smart enhancements to existing web standards. That's exactly
what happened with CSS and _animations_.

Many of the cool effects developers used to achieve with Flash, are now possible with CSS version 3. The idea is simple and
feels natural: you just define the steps of the animation in terms of CSS styling rules and the browser handles the
gradual transition from a step to the next. In fact, this is what developers already used to do via JavaScript: dynamic
changes to CSS rules. Now there's a standard syntax to do it inside the CSS stylesheet itself.

Here's an example of how to make a heading that continously enlarges and shrinks back to its original size:

``` css
@keyframes my_animation {
  0%   { font-size: 20px; }
  50%  { font-size: 30px; }
  100% { font-size: 20px; }
}

h1 {
  animation-name: my_animation;
  animation-duration: 4s;
  animation-iteration-count: infinite;
}
```

More on animations [here](http://www.w3schools.com/css/css3_animations.asp).

## What to do now

Styling with CSS definitevely is an art. Knowing a lot of properties and how they work is useful, but it's just tools. The point is
what to do with them. Go and search beatutiful web sites. Take inspiration.
