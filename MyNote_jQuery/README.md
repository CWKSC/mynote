# MyNote_jQuery

https://jquery.com/

https://www.w3schools.com/jquery/jquery_syntax.asp 

### 語法

```js
$(selector).action()
```

Examples:

`$(this).hide()` - 隱藏當前元素

`$("p").hide()` - 隱藏所有 \<p> 元素。

`$(".test").hide()` - 隱藏所有帶有 class =“ test” 的元素。

`$("#test").hide()` - 隱藏 id =“ test” 的元素。

___

document ready event

```js
$(document).ready(function(){
  // jQuery methods go here...
});
```

or short one

```js
$(function(){
  // jQuery methods go here...
});
```

這是為了防止文檔完成加載（準備就緒）之前運行任何jQuery代碼。

___

### jQuery Event

| Mouse Events | Keyboard Events | Form Events | Document/Window Events |
| :----------- | :-------------- | :---------- | :--------------------- |
| click        | keypress        | submit      | load                   |
| dblclick     | keydown         | change      | resize                 |
| mouseenter   | keyup           | focus       | scroll                 |
| mouseleave   |                 | blur        | unload                 |
| mousedown    |                 |             |                        |
| mouseup      |                 |             |                        |
| hover        |                 |             |                        |

https://www.w3schools.com/jquery/jquery_events.asp

`$(document).ready()`

___

### Get/Set content

- `text()` - Sets or returns the text content of selected elements
- `html()` - Sets or returns the content of selected elements (including HTML markup)
- `val()` - Sets or returns the value of form fields

___

### Add New HTML Content

- `append()` - Inserts content at the end of the selected elements
- `prepend()` - Inserts content at the beginning of the selected elements
- `after()` - Inserts content after the selected elements
- `before()` - Inserts content before the selected elements

___

### Remove Elements/Content

- `remove()` - Removes the selected element (and its child elements)
- `empty()` - Removes the child elements from the selected element

___

### jQuery Manipulating CSS

- `addClass()` - Adds one or more classes to the selected elements
- `removeClass()` - Removes one or more classes from the selected elements
- `toggleClass()` - Toggles between adding/removing classes from the selected elements
- `css()` - Sets or returns the style attribute

___

### Return a CSS Property

```js
css("propertyname");

$("p").css("background-color");
```

### Set a CSS Property

```js
css("propertyname","value");

$("p").css("background-color", "yellow");
```

### Set Multiple CSS Properties

```js
css({"propertyname": "value", "propertyname": "value", ...});

$("p").css({"background-color": "yellow", "font-size": "200%"});
```

___

### jQuery Dimension Methods

- `width()`
- `height()`
- `innerWidth()`
- `innerHeight()`
- `outerWidth()`
- `outerHeight()`

https://www.w3schools.com/jquery/jquery_dimensions.asp

___

### jQuery .attr() vs .prop()

https://cythilya.github.io/2017/09/10/jquery-attr-vs-prop/

https://stackoverflow.com/questions/5874652/prop-vs-attr

Return the value of a property:

```js
$(selector).prop(property)
```

Set the property and value:

```js
$(selector).prop(property,value)
```

Set property and value using a function:

```js
$(selector).prop(property,function(index, currentvalue))
```

Set multiple properties and values:

```js
$(selector).prop({property:value, property:value, ...})
```

