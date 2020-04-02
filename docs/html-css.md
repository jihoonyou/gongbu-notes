# html-css

## What is HTML?

- Hyper Text Markup Language
- HTML documents are described by HTML tags
```
<!DOCTYPE html>
<html>

    <head>
    
    </head>
    
    <body>
    
    </body>

</html>
```

Doctype  This is technically not an HTML element, but an instruction to the browser about what version of HTML the page is written in.
The head element can include a title for your web site. CSS styles, some information for the browser or for search engines and more.

The body element is where all the visible stuff of your web page goes, like all the content such as text, links, images, lists, and many more elements.

```
<p></p>
<strong></strong>
<em></em>
<u></u>
<br>
<img src='___' alt=">
<a href="" target="_blank"></a>
```

Paragraphs are elements for larger texts.
Strong tag for bold
em for emphasize -> italic
u -> underline

What is an attribute?
- Additional informatino about an element

Attributes provide additional information about an element.
Should give the img elements an alt attribute.
- alternative text for the image

link tag with <a> tag anchor
- target="_blank" on anchor tag will open the link on new tab
- internal link - link to documents
- external link - A link to a website that isn't part of our project

How many different heading (such as h1) elements are there?
- 6

## What is CSS?
Cascading Style Sheets
Css defines exactly how HTML looks like
- seperation between content and style
- HTML is content // CSS style

three ways to use css
- css code right inside an HTML tag with style attribute
- css code inside an HTML document with style element
- css code in external file

each rule consists of a selector and a declration block

```
body {
    font-family: Helvetica Neue, Arial;
    font-size: 18px;
}

h1, h2 {
    color: green;

}
h1 {
    font-size: 40px;
}

h2 {
    font-size: 25px;
}
p {

    text-align: justify;
}
```
css inheritance
- child elements inherit the properties from their parent elemnts 
- unless we overwrite their styles

css color
- #RRGGBB
- 0-255 -> ff
- rgba(0,0,0, 0.75) transparency

```
<p class="">
<p id="">
```
class can be attributed to as many element as you want -> .
id can be attributed to only once to each element      -> #
- using id is not a good practice so try to use class
