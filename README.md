## Jade Styleguide

### No unnecessary divs

Unspecified elements are automatically cast as a `div`, so don't waste space specifying one.

```jade
//- BAD
div.class

//- GOOD
.class
```

### No commas in attributes

Don't add unnecessary commas to attributes.

```jade
//- BAD
form(method="", action="")

//- GOOD
form(method="" action="")
```

### No unnecessary interpolation or parentheses

Do use string interpolation where it makes sense, but not for strings or content that will be placed directly into the element. Don't wrap conditions in parentheses when it's not
necessary.

```jade
//- BAD
.class(class="class-" + i)
//- GOOD
.class(class="class-#{i}")

//- BAD
.class(data-id="#{model._id.toString()}")
//- GOOD
.class(data-id=model._id.toString())

//- BAD
.class #{content}
//- GOOD
.class= content

//- BAD
.class(class=(condition ? "class-1" : "class-2"))
//- GOOD
.class(class=condition ? "class-1" : "class-2")
```

### Wrap many attributes

If attributes won't fit easily on one line, wrap all attributes with the same indentation, closing the brackets on the following line to make current indentation clear.

```jade
//- GOOD
input.class(
  type="text"
  placeholder="Text Input"
  name="text"
  value=condition ? value1 : value 2
  required
)
```

### Iterate when appropriate

Iterate over arrays or object where it makes sense, even if variables must be created on the fly. Use common sense to determine if the data is best passed to the template.

```jade
//- GOOD, but remember that "j" is undefined
for j, i in new Array(99)
  .char(class="#{char}-i")= i

//- OK, but prefer passing menu object to template
- var menu = {"Home": "/home", "Settings": "/settings", "Log out": "/logout"};
for url, text in menu
  a(href=url)= text
```
### Prefer native jade

Use native `for` and `if` directives rather than JS blocks.

```jade
//- BAD
- for (var i = 0; i < arr.length; i++) {
  span= i
- }

//- GOOD
for el, i in arr
  span= i
```

### Prefer double quotes

Make code consistent with our CoffeeScript styleguide by preferring double quotes.

```jade
//- BAD
form(method='POST' action='')

//- GOOD
form(method="POST" action="")
```

### Use valid HTML

Don't create custom attributes or nest invalid elements. Never use IDs inside of a loop.

```jade
//- BAD
.class(customattribute=thing)

//- GOOD
.class(data-attribute=thing)

//- BAD
ul
  h1 Title
  p Paragraph text.

//- BAD
p
  .class

//- BAD
for item in array
  #array-item= item
```

### Reduce unnecessary duplication

Don't place conditions at the top level when they can be nested further down.

```jade
//- BAD
if condition
  .class
    p
      = value1
else
  .class
    p
      = value2

//- BETTER
.class
  p
    if condition
      = value1
    else
      = value2

//- BEST
.class: p
  = condition ? value1 : value2
````

### Nest short lines

Nest short lines when they have consistent features and fit over one line.

```jade
//- GOOD
ul
  li.class: a.link(href="/link-1") Link 1
  li.class: a.link(href="/link-2") Link 2
  li.class: a.link(href="/link-3") Link 3
```

### No JS event handlers inlined

Don't attach event handlers inside Jade, whose purpose is only to mark up the document.

```jade
//- BAD
img(onerror="")
```
