---
title: Dynamic Binding of Classes and Styles in Vue.js!
date: "2019-08-27T21:45:00.000Z"
description: "There will be a lot of situations where the classes and styles attached to a node will have to be dynamic. Let's see how it's done."
---

We know how to attach classes to a tag. But what if we want to do so dynamically. For this we can use the <code>v-bind</code> directive with <code>class</code>. <code>v-bind</code> can be used along with <code>style</code> to apply styles dynamically.

## Classes

#### Object Syntax

We pass an object to <code>v-bind:class</code> where the key is the name of the class and the value is a boolean to decide whether we want to display the class or not.

```html
<div class="box" v-bind:class="{ active: isActive }"></div>
```

So if isActive is <code>true</code>, the class <code>active</code> gets attached to the node.

We can also have multiple classes by having more fields in the object that is being passed. For the given template,

```html
<div class="box" v-bind:class="{ active: isActive, redBorder: hasError }"></div>
```

And the following data,

```javascript
data: {
  isActive: true,
  hasError: false
}
```

The rendered node will look like this.

```html
<div class="box active"></div>
```

When <code>hasError</code> become <code>true</code>, <code>hasError</code> class will get tagged on.

The object doesn't have to be inline. It can be stored in data and then be accessed in the template. We could also use the computed property to return the object.

```html
<div class="box" v-bind:class="classObject"></div>
```

```javascript
data: {
  classObject: {
    active: true,
    redBorder: false
  }
}
```

Or with computed properties:

```javascript
data: {
  isActive: true,
  hasError: false
},
computed: {
  classObject: function() {
    return {
      active: this.isActive,
      redBorder: this.hasError
    }
  }
}
```

#### Array Syntax

We can also pass classes to a node by an array. This is extremely useful when we have a list of classes to apply.

```html
<div class="box" v-bind:class="[ activeClass, errorClass ]"></div>
```

```javascript
data: {
  activeClass: 'active',
  errorClass: 'redBorder'
}
```

This will render:

```html
<div class="box isActive hasError"></div>
```

You could also have objects in these arrays which can be useful in case of dynamically attaching classes.

```html
<div class="box" v-bind:class="[ { active: isActive }, errorClass ]"></div>
```

```javascript
data: {
  isActive: true,
  errorClass: 'redBorder'
}
```

## Inline Styles

#### Object Syntax

Similar to the case of classes, we can pass an object to <code>v-bind:style</code>. CSS properties can be either camelCase or kebab-case(mention within quotes).

```html
<div class="box" v-bind:style="{ backgroundColor: currentColor, fontSize: fontSize + 'px' }"></div>
```

```javascript
data: {
  currentColor: 'red',
  fontSize: 30
}
```

You could also bind style through an object from data property or through a computed property that returns an object.

```html
<div class="box" v-bind:style="styleObject"></div>
```

```javascript
data: {
  styleObject: {
    backgroundColor: 'red',
    color: 'white'
    fontSize: 30 + 'px'
  }
  
}
```

#### Array Syntax

We can also pass multiple style objects to <code>v-bind:style</code> with the help of an array.

```html
<div class="box" v-bind:style="[ blandStyle, dashingStyle]"></div>
```

---

As an exercise, you could create events to change the colour of the background and text of a div. For example, a click event changes the colour of a div from red to green and back and forth. And to take a step further, try creating a progress bar! Good luck!