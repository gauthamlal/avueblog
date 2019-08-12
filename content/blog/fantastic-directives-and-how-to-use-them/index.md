---
title: Fantastic Directives and How To Use Them!
date: "2019-08-12T22:00:00.000Z"
description: "Directives are attributes provided by Vue that can help us apply a special behavior on to our HTML."
---

Welcome to another edition of A Vue Blog, a blog for beginners to Vue.js from a beginner to Vue.js. Last time we saw how to print **Hello World!** on to the screen using string interpolation. Let's move forward and look into directives.

Directives are attributes provided by Vue that can help us apply a special behavior on to our HTML and DOM. They all start with <code>v-</code> which indicates that they are provided by Vue.

We can create our own directives but in this article, we will play with some of the default directives which can be most useful.

## <code>v-bind</code>

Let's try and create a link that takes us to the [blog](https://evanyou.me) of the creator of Vue.js, Evan You. We will create a property called <code>url</code> inside the data property and try to pass it to the <code>href</code> attribute of the anchor tag using templates.

```javascript
let app = new Vue({
  el: '#app',
  data: {
    message: 'Hello World!',
    
    : 'https://evanyou.me'
  }
});
```

```html
<div id="app">
  <a href="{{ url }}">Evan You's blog!</a>
</div>
```

Then you go ahead and click the link, but it doesn't take you to the URL. This is because templates don't work with attributes. 

Inorder to use properties inside attributes, we use a directive called <code>v-bind</code>. 

```html
<div id="app">
  <a v-bind:href="url">Evan You's blog!</a>
</div>
```

And now the link takes you to the URL in the data property.

## <code>v-once</code>

<code>v-once</code> is a directive which forces a tag to render only once. Now any time the value of <code>message</code> changes, the rerender will not occur.

```html
<div id="app">
  <h1 v-once>{{ message }}</h1>
</div>
```

You can try to reassign <code>app.message</code> a new value, but the output will not change.

## <code>v-text</code>

This directive does what template syntax does. Show the value of a data property.

```html
<h1 v-text="message"></h1>
```

## <code>v-html</code>

Vue.js by default escapes HTML. What this means is that if we use templates to print a property that contains HTML, it will get printed as text and not as a tag. This protects the program from [XXS attacks](https://www.owasp.org/index.php/Cross-site_Scripting_(XSS)).

In case we need to output HTML, we use <code>v-html</code> directive.

```html
<span>{{ htmlToDisplay }}</span>      <!-- <p>Hey fellas!</p> -->
<span v-html="htmlToDisplay"></span>  <!-- Hey fellas! -->
```

## <code>v-model</code>

This directive can be used to create two-way data bindings on form input, select and other elements. It lets us update data properties on user inputs.

```html
<input v-model="message" placeholder="Edit the message">
<p>Message is: {{ message }}</p>
```

The initial message shown will be 'Hello World!'. The input field will also have the same value. When you edit the input field, you will see the same changes getting reflected below.

## <code>v-if, v-else </code> and <code>v-else-if</code>

Vue has provided directives for conditional rendering. This helps us to render only when a given condition is satisfied.

```html
<p v-if="showThem">Hey Guys!</p>
```

The above tag will only get rendered when <code>showThem</code> is true.

## <code>v-for</code>

This directive lets us print a list of items. 

```html
<ul>
  <li v-for="fruit in fruits">{{ fruit }}</li>
</ul>
```

```javascript
let app = new Vue({
  el: '#app',
  data: {
    fruits: [
      'Apple',
      'Orange',
      'Grape'
    ]
  }
});
```

This will render an unordered list of fruits.

## <code>v-on</code>

<code>v-on</code> directive lets us listen to DOM events and execute a piece of code when the event gets triggered.

```html
<div>
  <button v-on:click="count += 1">Increment by 1</button>
  <p>
    The count is: {{ count }}
  </p>
</div>
```

```javascript
let app = new Vue({
  el: '#app',
  data: {
    count: 0
  }
});
```

On every <code>click</code> event on the button, the data property, <code>count</code> gets incremented by 1. We see the change getting reflected below where we display the <code>count</code>.

There are many more ways we can use the <code>v-on</code> directive and we will look at them in the future.

---

Vue.js instances can not only have data properties. They can also be home to **methods**. And that's what we will get into next time!