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

## elements
### terminology
**element**, a syntax that changes how some text renders/functions

**inline**, inside a paragraph

**independent**, on their own line

### comments
```markdown
// these are comments
// they will not be rendered

/*
	this is a multiline comment
	it will also not be rendered
*/
```

### paragraphs
```markdown
for normal text/a paragraph you just write characters.
putting text in the following line with only one newline between them should produce a small margin between the the two paragraphs.

putting text in the following line with two or more newlines between them should produce a large margin between the two paragraphs.
```

### headers
```markdown
// these should - by default, be rendered as bold
// these should be bigger then normal text
# this is a primary header, i am biggest
## this is a secondary header, i am big
### this is a tertiary header, i am medium

// this should be the same size as normal text
#### this is a quaternary header, i am small

// these should be smaller then normal text
##### this is a quinary header, i am smaller
###### this is a senary header, i am smallest.

// if the url ends with the anchor #custom, the page will automatically scroll down to this header
// the {#...} element replaces the default anchor that is generated from the header's content with a custom defined one
# this header has a custom anchor {#custom}
```

### text styles
```markdown
// these can be nested
// and can be used for parts of a paragraph too
_this is an italic paragraph_
*this is an italic paragraph*
**this is a bold paragraph**
__this is an underlines paragraph__
~~this is a strikethrough/redacted paragraph~~
`this is a monospace paragraph`
```

### notes
```markdown
> this is a note, it must have a space after the closing pointy bracket
>
> the same principals as paragraphs apply to notes
```

### lists
```markdown
// ordered list with numbers
1. item one
2. item two
2.5. item two and a half

// ordered list with letters
a. item one
b. item two

// ordered list with roman numerals
// if there is a list that ends with h. immediately before this one, then it would be invalid and counted as a part of the ordered list with letters.
i. item one
ii. item two

// unordered list
- potatoes
- eggs
- gluten

// task list
- [x] finished task a
- [x] finished task b
- [ ] unfinished task
```

### code blocks
	```
	multiline

	code
	block
	```

	```bash
	# multiline code block
	# with bash syntax highlighting
	```

### hyperlinks
```markdown
// a regular hyperlink
// can be placed both inline or independent
[link](telarum://id.name/)
// an address hyperlink
// a hyperlink that has the same name and href
// works for email addresses too
<telarum://id.name>

// a reference hyperlink
[reference][1]
// the hrefs for reference hyperlinks are stored independently somewhere else on the page
[1]: telarum://id.name/
```

### multimedia
```markdown
// a footnote
// similar to reference hyperlinks, but the href is a paragraph inside the same document
[footnote][^1] and a [long footnote][^2]
// to attach multiple paragraphs to a footnote, make sure to indent them
[^1]: duis tincidunt velit mauris
[^2]: lorem ipsum dolor

	sit amet consectetur adipiscing elit


// a button
// can be placed independently, or inline only with other buttons
(button)(telarum://id.name/)

// tells the browser that it should put image.png here
![image](telarum://id.name/image.png)
```

### layout
```markdown
// horizontal line separator
// three (or more) dashes or underscores on their own line
---
___


// term definitions
// ie. rarely used <dl> element in html
inline
: inside a paragraph
independent
: on their own line
: and also pee pee

// table
// first/last pipes can be omitted
// there has to be at least one dash in the "second" row to have a table rendered as a table
// by default columns are left aligned, but you can change the alignment with colons in the "second" row, :- aligns left, :-: aligns center, and -: aligns right
| row 1 | col 2 |
| ----- | ----- |
| row 2 | col 2 |
| row 3 | col 2 |
```
