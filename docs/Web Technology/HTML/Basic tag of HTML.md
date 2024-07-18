### Heading tag

heading tag is a predefined text that is used in HTML to print a text which is bigger in size and bolder in weight compared to normal text.
There are 6 type of heading tags, starting from h1 to h6. h1 is biggest

Example:
```HTML
<h1>Welcome to Jspider</h1>
<h2>Welcome to Jspider</h2>
<h3>Welcome to Jspider</h3>
<h4>Welcome to Jspider</h4>
<h5>Welcome to Jspider</h5>
<h6>Welcome to Jspider</h6>
```

#### OUTPUT
<h1>Welcome to Jspider</h1>
<h2>Welcome To HTML</h2>
<h3>Welcome To HTML</h3>
<h4>Welcome To HTML</h4>
<h5>Welcome To HTML</h5>
### Paragraph Text

paragraph tag(`<p></p>`) is a HTML text that is used to create an empty line before starting the paragraph and after ending the paragraph.

Example
```html
Welcome to Jspider
<p>Welcome to Jspider</p>
Welcome to Jspider
```
#### OUTPUT

Welcome to Jspider
<p>Welcome to Jspider</p>
Welcome to Jspider

### Break

break is a single tag that is used in html to break the line in the middle on text and move the content to next line.

Example:
```html
<br> -> used to apply break
<p>Welcome <br> to HTML</p>
```
#### OUTPUT
<p>Welcome <br> to HTML</p>
### Anchor Tag

```HTML
<a href ="./Second Page" target ="_self or _blank or iFrame_id"/>
Next page
</a>
```
Anchor tag is to use for navigate from one html page to other html page.
Properties
- href : it is a properties of anchor tag which is used to mention the address of another html page.
- target: it is a properties of anchor tag which is used to specify the target of new page.
	Target values are:
	- _self : to open new page on the same tags.
	- _blank : to open new page on the new blank tab and leaves the correct tab blank._
Example 

<a href=""  target="_self">This text appears hyperlink</a>

### Image tag

```html
<img scr = "" alt = "">
```
- img tag is a single tag used in html to display an image on a webpage.
- img tag can be used to display the collection of multiple images in various dimension on single webpage.
Properties 
- 'src' : src stand for Source, src is used to mention the address of image.
	Ways of addressing the image.
	1.  "./image.jpg"
	2. "../image.jpg"
	3. Copy image address from browser.
- 'alt' : stand for alternative,
	- alt is used to write a message if source is not working properly.
- height: used to change height of image vertical length of image.
- Width: used to change the horizontal size of image.
Example
```html
<img src="./image.jpg" alt="Show text if source not working"
	 width="200" height="100">	 
```
height and width take number value inside double quotes. 
