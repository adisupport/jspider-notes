CSS stand for Cascading Style Sheet.
CSS is a styling library that was introduce in the year 1995.
CSS is used to apply the properties like 
- Structuring
- reshaping
- resizing
- styling
- designing 
- transforming
- positioning the content of HTML.
#### Advantage of CSS
- Styling is done for individual element and collection of element also.
- easy to select particular element in css.
- CSS library has update to new version CSS3 which allow user to build responsive web page with the help of media query and animation properties.
### Ways to use CSS
1. Inline
2. Internal 
3. External
### Inline CSS

Inline CSS stands for in the line of tag, it is a way of writing css for particular elements inside the tag itself.
Inline CSS uses a property known as style = " " in which we write the CSS.
e.g : 
```CSS
<body>
	<h1 style = "background-color:aqua; color:blue;" >Welcome to CSS</h1>
</body>
```

***OUPUT***

<body>
	<h1 style = "background-color:aqua; color:blue;" >Welcome to CSS</h1>
</body>

### Internal CSS

Internal CSS is a way of writing CSS inside of a HTML page itself.
In internal CSS styling should written only inside of `<head></head>` tag itself.
In internal CSS we use `<style></style>` to apply the styles.

#### Syntax

```html
<html>
	<head>
		<style>
			selctor{
				property:value;
				property:value;
				property:value;
				..............
				.............
				.......
				....
			}
		</style>
	</head>
</html>
```

***Example*** 
```html
<style>
	h1{
		background-color:aquamarine;
		color:red;
	}
</style>
```

### External CSS

External CSS is a method to writing CSS in a separate style sheet out of html page.
in external CSS we can use two separate pages for html and CSS to connect these two html and CSS file.
- inside `<head></head>` tag we use `<link rel="stylesheet" href="address of css file">`

```
<head>
	<link rel = "stylesheet" href="./style.css">
</head>
```
#### Link has two properties
1. 'rel' : stands for relation that is used to specify the type of relation with the html.
	e.g:
		rel = "stylesheet"
		rel ="icon"
		rel ="script"
2. 'href' : to mention the address of other file which you want to associate.

Example of external CSS

```external.css file
h1{
	color:white;
	background-color:blue;
}
```

```index.html file
<body>
	<h1>Welcome to CSS</h1>
</body>
```


