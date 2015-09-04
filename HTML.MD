# Learn HTML in 10 minutes

I lied. Again. You can't learn HTML in 10 minutes. But you can get the gist of it.
Then buy a 900pages book or read a lot of stuff online. Eventually you'll find that
you need to do both. Maybe more than once. It depends on what you want to do or become.
HTML is used for the web, and the web changes fast and changes a lot.

## Tags

HTML stands for _HyperText Markup Language_. Hypertexts are textual contents linked to each other.
Think of a book that let's you jump from a page to another, or even to a different book.
Markup is a technique used to express how textual content is structured. It's based on the concept of _tag_.

A tag has a name and can be either an opening tag or a closing tag. In HTML tags are indicated wrapping
their names into _angle brackets_ and a closing tag is written with a slash before its name. So this is
an example:

``` html
<p>Hi, this is an example</p>
```

In this case `p` is the tag name, we got an opening `p` and a corresponding closing `p`. In between there is some text.
In general, tags can contain text, other tags and any combination of text and tags. Also, you can have empty tags: an opening
tag immediately followed by its matching closing tag. Every HTML tag has a purpose. Some tags, due to their purpose, don't
require a matching closing tag.

An _element_ is an opening tag with is matching closing tag (if present) and its content (if present).
The terms "element" and "tag" are often used as synonyms.

## Head and body

This is the basic stucture of an HTML document:

``` html
<html>
  <head>
  </head>
  <body>
  </body>
</html>
```

You always put everythint inside an `html` tag. Inside this tag, you put a `head` tag and a `body` tag.
`head` will contain important stuff _related_ to the content, while `body` will contain the content itself.
For now, we'll focus on what to put inside `body`, then I'll show what `head` is used for.

## Text content

HTML was originally designed to serve text content. Its purpose was to express both the content and its structure. As I said,
tags express the structure. Using specific tag names, you can also give a hint of what the element will contain. Technically
speaking, there are a couple of _semantic tags_, like `p`, which is used to wrap the text of a paragraph within a section of
the document. Here is a richer example:

``` html
<html>
  <head>
  </head>
  <body>
    <h1>Title of the page</h1>
    <h2>Subtitle</h2>
    <h3>A section title</h3>
    <p>First paragraph.</p>
    <p>Second paragraph.</p>
  </body>
</html>
```

I suggest you to try to test this HTML code. You can do it by opening your favorite text editor
(I suggest you [Sublime Text](http://www.sublimetext.com/), but even Windows Notepad will do), pasting
the code inside a new file and save the file with the `.html` extension. Finally, open the file with your web browser.
If you're lazy, you can see the code in action [here](https://jsfiddle.net/bsL97a90/).

**Note:** Use a text editor, not a word processor. Examples of word processors are Microsoft Word and OpenOffice.org Writer.
Word processors add hidden information to your files, needed to express how to style text (which font, size, color, ...).
In order to do this, they use file formats that web browsers are not expected to (and usually don't) understand.

Here is a list of the most used text-relaed semantic HTML tags:

* `h1`, `h2`, `h3`, `h4`, `h5`, `h6` for _headings_ (a heading is a sort of title for a section;
`h1` is usually used as a general title for the whole HTML docuent, while `h2` and the others are
for sections and sub-sections)
* `p` is for paragraphs
* `strong` and `em` are used to stress the importance of one ore more words
(`strong` text is usually rendered by web browsers as bold, while `em` is rendered
as italic)
* `br` is used as a line terminator and doesn't require a matching closing tag
* `ul`, `ol` and `table` are for lists, numbered lists and tables
(you may want to check the details [here](http://www.w3schools.com/html/html_lists.asp)
and [here](http://www.w3schools.com/html/html_tables.asp))

## Multimedia

Today HTML is used for a lot of stuff it wasn't originally designed for. Notably, multimedia content.
Pictures came early, with the `img` tag. Here is an example:

``` html
<img src="https://www.google.com/images/srpr/logo11w.png">
```

A couple of notes here. First, you don't need to close the tag. Second, you tell where to get the picture with the
`src` _attribute_. Attributes are data you attach to an opening tag. Every attribute has a name and often it also has
a value. In the example tha name is `src` and the value is `https://www.google.com/images/srpr/logo11w.png`.

After picures, we got music and videos. For many years, these kinds of content have been handled by external plugins,
and HTML didn't provide dedicated tags. Now with HTML5 we have `audio` and `video` tags. You may want to see the
details [here](http://www.w3schools.com/html/html5_audio.asp) and [here](http://www.w3schools.com/html/html5_video.asp).

## Links

HTML documents can link to other HTML documents of, more generally, to other resources. Links are
indicated with the `a` tag:

``` html
<a href="https://www.google.com/">Go to Google</a>
```

## DIV and SPAN

HTML content is frequently sectioned with `div` and `span` tags. They aren't designed for a particular kind
of content. Tecnically speaking, they aren't _semantic tags_. Still, they are useful to structure content.
They are often used with `id` and `class` attributes. Let's see an example first:

``` html
<html>
  <head>
  </head>
  <body>
    <div id="page_header">
      <h1>Title of the page</h1>
      <h2>Subtitle</h2>
    </div>
    <div id="page_main_content">
      <div class="section">
        <h3>A section title</h3>
        <p>First paragraph.</p>
        <p>Second paragraph.</p>
      </div>
    </div>
  </body>
</html>
```

`div` and `span` differ in that `div` is intended for a content spanning all available width,
forcing surrounding content to be put on different lines; multiple `span`, instead, can live toghether on the same line.

The `id` attributes provide identifiers (i.e. unique names) for elements. The `class` attribute assigns
the element to one or more categories called _classes_. These attributes are useful when you add CSS
and JavaScript to your HTML document. For now, just know that they exist and they are used in almost
every HTML document.

**Note:** The new [HTML5 semantic tags](http://www.w3schools.com/html/html5_semantic_elements.asp) are often
good alternatives to `div` and `span`.

## What is &lt;head&gt; for?

`head` is used mostly for:

* declare the character set used in the document (usually UTF-8)
* provide a title and / or an icon that web browsers can use to customize the tab displaying your document
* link your document to a CSS stylesheet
* link your document to a JavaScript program

Here is a snippet of `<head>` code in HTML5:

``` html
<head>
	<meta charset="UTF-8">
	<title>Put your title here</title>
	<link rel="shortcut icon" href="img/favicon.png">
	<link href="css/commons.css" rel="stylesheet">
	<script src="js/commons.js">
</head>
```

**Note:** This syntax is for the 5th version of HTML. Older versions are more verbose. In general I recommend you
to write HTML5 code and let old versions go. HTML5 is still work in progress, but web browser already offer excellent
support for most features.

## Comments

Sometimes is useful to leave a message to readers of your HTML code, yourself included. For example
you may want to visually separate portions of HTML code with comments at the beginning that hints
at what the following code is for.

Web Browsers ignore comments. In other words, comments won't affect how your document is rendered.

Here is an example of HTML comment:

``` html
<html>
  <!-- This is a comment. -->
  <head>
    <!-- This comment highlights the start of a head element. -->
  </head>
  <body>
    <!-- This comment highlights the start of a body element. -->
  </body>
</html>
```

## Doctype declaration

For historical reasons the first line of an HTML document should say that it... is an HTML document.

You do this through a _doctype declaration_. Older versions where very verbose, but in HTML5 the doctype declaration
is simply:

``` html
<!DOCTYPE html>
```

After the declaration goes the rest of the HTML code.

## A couple of words about CSS and JavaScript

What you have learned so far allows you to create documents with various kind of content and structure. But
the resulting web pages will always be _static_. In other words, content and structure will remain the same,
not allowing the user to interact. Also, the look of your page will probably be pretty simple, because the
browser will apply its standard format settings.

CSS and JavaScript address these problems. CSS is a language designed to describe how your document has to be
styled. JavaScript is a programming language that browsers understand and that you can use to change both
the content and the structure of your document in response to user-generated events, thus allowing interactivity.

You got to learn this stuff, otherwise your web sites will look like '90s web sites.

## What to do now

Try the [W3C Schools HTML tutorial](http://www.w3schools.com/html/default.asp) or
[search](https://www.google.com/cse?cx=013493258683483688568:xhfa6ctm1ki&q=html#gsc.tab=0&gsc.q=html&gsc.page=1)
a good book. I can't suggest you a specific title. I believe that HTML has to be learned mostly with practice.
Reading a book is useful but keep in mind that things changes fast and there is a lot
of stuff to know. Books evolve slowly and have limitations that web doesn't have. So start with a simple project
and try to learn new things by yourself each time your project's evolution requires it. Google can help you:
be smart at understanding what you need and how to search it. This is a key skill for a web developer.
