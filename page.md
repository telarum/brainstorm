---
author: zvava
---

# page

- what is page?

`page` is name of the markup language used by telarum. it is largely inspired by the principals of markdown, which means it should be easily readable in raw form, and intuitive to write in. there should be no elements in the tradition sense of `<elem>` or `{{ elem }}` at all, only markdown-y representations. page is supposed to provide a ~~superior~~ alternative markup format to html.

> by markdown-y representations i mean `# header` over `{{ h1 | header }}` and `<h1>header</h1>`, or `[title](location)` over `{{ link | title | location }}` and `<a href="location">title</a>`.

- what about elements?

there should be no elements in the traditional sense, there should be a set amount of "elements" so that they can be consistently themed by the client and no possible way of having a unique theme on a website.

- what do you mean no unique styles?

oh yeah, where page replace html, there is nothing to replace css, and definitely nothing to replace js &mdash; read on.

## page over html

page should provide only the content and some basic layout, you - the user with your client, should provide the style, and have complete freedom over how you want to interpret the page. this is a superior approach because;

1. the page is always semantic, improving accessability, over the divided* nature of the "modern" web.

*many sites use divs with classes/ids for every element, or use custom elements, etc. instead of sticking with semantic html

2. the page is always static**, improving performance, over the dynamic nature of the "modern" web. this also improves security as the server cannot load tracking scripts or ads.

**the server has to serve static text, there is no possibility of the server serving javascript so it can serve you for a second time, this time actually with the content. static in this sense does not mean the page cannot change between requests

3. pages are consistently styled, allowing you to have a universal dark/light/solarized/idgaf theme instead of having to mess with multiple userstyles or extensions. websites already look exactly how you want.

4. (in addendum to 3) because page is designed to be alike to markdown, you can also just browse raw pages in a terminal*** and have pretty much the same experience as with a gui client.

***with or without a dedicated tui client to eg. allow you to easily follow links
