## Jade Styleguide

### No unnecessary divs

Unspecified elements are automatically cast as a `div`, so don't waste space specifying one.

```jade
  div.class                                           //- BAD
  .class                                              //- GOOD
```

### No commas in attributes

Don't add unnecessary commas to attributes.

```jade
  form(method="", action="")                          //- BAD
  form(method="" action="")                           //- GOOD
```

### No unnecessary string interpolation or parentheses

Don't use string interpolation for strings or content that will be placed directly into the element. Don't wrap conditions in parentheses when it's not
necessary.

```jade
  .class(data-id="#{model._id.toString()}")           //- BAD
  .class(data-id=model._id.toString())                //- GOOD

  .class #{content}                                   //- BAD
  .class= content                                     //- GOOD

  .class(class=(condition ? "class-1" : "class-2"))   //- BAD
  .class(class=condition ? "class-1" : "class-2")     //- GOOD
```

### Wrap many attributes

If attributes won't fit easily on one line, wrap all attributes with the same indentation, closing the brackets on the following line to make current indentation clear.

```jade
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

  // - OK, but prefer passing menu object to template
  - var menu = ["Home", "Settings", "Log out"];
  for item in menu
    - var url = "#" + item.replace(" ", "-").toLowerCase();
    a(href=url)= item
```
### Prefer native jade

Use native `for` and `if` directives rather than JS blocks.

```jade
  - for (var i = 0; i < arr.length; i++) {          //- BAD
    span= i
  - }

  for el, i in arr                                  //- GOOD
    span= i
```

### Prefer double quotes

Make code consistent with our CoffeeScript styleguide by preferring double quotes.

```jade
  form(method='POST' action='')                     //- BAD
  form(method="POST" action="")                     //- GOOD
```

### Use valid HTML

Don't create custom attributes or nest invalid elements.

```jade
  .class(custom-attribute=thing)                    //- BAD
  .class(data-attribute=thing)                      //- GOOD

  ul                                                //- BAD
    h1 Title
    p Paragraph text.

  p                                                 //- BAD
    .class
```

### Reduce unnecessary duplication

Don't place conditions at the top level when they can be nested further down.

```jade
  if condition                                     //- BAD
    .class
      p
        = value1
  else
    .class
      p
        = value2

  .class                                           //- BETTER
    p
      if condition
        = value1
      else
        = value2

  .class: p                                       //- BEST
    = condition ? value1 : value2

````

### Nest short lines

Nest short lines when they have consistent features and fit over one line.

```jade
  ul
    li.class: a.link(href="/link-1") Link 1
    li.class: a.link(href="/link-2") Link 2
    li.class: a.link(href="/link-3") Link 3
    li.class: a.link(href="/link-4") Link 4
    li.class: a.link(href="/link-5") Link 5
```

### No JS event handlers inlined

Don't attach event handlers inside Jade, whose purpose is only to mark up the document.

```jade
  img(onerror="")                               //- BAD
```
