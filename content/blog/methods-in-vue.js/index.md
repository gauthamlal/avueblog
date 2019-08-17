---
title: Methods in Vue.js
date: "2019-08-14T23:30:00.000Z"
description: "Here is how we provide methods to our Vue instances."
---

Vue instances can have methods defined in it along with data instances. In this article, we will look into the 'methods' property of the Vue instance.

## Methods

The method property is where we define the functions that are to associated with the Vue instance. They are very useful for providing functionalities to directives, events or to get work done like regular reusable functions.

Let's give this a test by creating a function to call alert when a button is clicked.

```javascript
let app = new Vue({
  el: '#app',
  data: {
    message: 'ALERT!'
  },
  methods: {
    callAlert: function() {
      alert(this.message);
    }
  }
});
```

```html
<div id="app">
  <button v-on:click="callAlert">Click me!</button>
</div>
```

Here we let the button know to call <code>callAlert()</code> function when it's click event is triggered using the <code>v-on</code> directive. (You can go [here](https://avueblog.netlify.com/fantastic-directives-and-how-to-use-them/) to get a quick refresh on directives)

We don't have to call a function as <code>v-on:click="callAlert()"</code>. This is unnecessary. <code>v-on:click="callAlert"</code> will suffice.

Then we go ahead and define the <code>callAlert</code> function inside the methods property of the Vue instance.

Now we want to show the value stored in the <code>message</code> data property in the alert box. We can access data properties inside methods using the <code>this</code> property. So, in this case, we can access the value of <code>message</code> using <code>this.message</code>. And that's how we pass the value of <code>message</code> to the alert box.

There we go! We just called our very first method in Vue!

And this demonstrates how useful methods are in the case of event handling in Vue.js.

## Passing Parameters

Like normal functions, Vue.js methods can also accept parameters. <code>v-on:click="methodName(param)"</code> is how we can pass parameters to methods. Let's try to expand this on our previous example.

```javascript
let app = new Vue({
  el: '#app',
  methods: {
    callAlert: function(textMessage) {
      alert(textMessage);
    }
  }
});
```

```html
<div id="app">
  <button v-on:click="callAlert('Parameter says hi!')">Click me!</button>
</div>
```
<br />

---

You can access the event object the way you usually do in normal Javascript functions.

But in case you need to accept another parameter along with the event object, we pass a keyword reserved by Vue in the method call, <code>$event</code>.

```html
<input type="text" v-on:keydown="storeValue('Mr.', $event)">
<p>{{ value }}</p>
```

```javascript
new Vue({
  el: '#exercise',
  data: {
    value: ''
  },
  methods: {
    storeValue: function(salutation, event) {
    	this.value = salutation + ' ' + event.target.value;
    }
  }
});
```

Here the output will have the salutation passed to the method, which we attach to the value.

## Event and Key Modifiers

Calling <code>event.preventDefault</code> or <code>event.stopPropogation</code> inside event handlers is very common. Vue lets us skip this step of calling them inside the event handlers and thus have only data logic inside it. Vue provides event modifiers which can be postfixed with a dot after the <code>v-on</code> directive.

```html
<!-- the propagation of the click event  will be stopped -->
<a v-on:click.stop="handleClick"></a>

<!-- the form submit event will no longer cause a reload of the page -->
<form v-on:submit.prevent="onFormSubmit"></form>
```

There are many other event modifiers like <code>.capture</code>, <code>.self</code>, etc. You can [check them out in the official docs](https://vuejs.org/v2/guide/events.html#Event-Modifiers).

---

Key Modifiers on the other hand lets us listen for specific keys during keyboard events. 

```html
<!-- `handleInput()` will only be called when the key is `Enter` -->
<input v-on:keyup.enter="handleInput">
```

This can help us in cases where we want to change a data property only when enter is pressed. You can find many more [key modifiers in the official docs](https://vuejs.org/v2/guide/events.html#Key-Modifiers).

---

Now that we have got our heads around Vue methods, it's time for a challenge. Remember that we set up a counter that increments on every button click in the last [post](https://avueblog.netlify.com/fantastic-directives-and-how-to-use-them/)? Now you could try to do that with Vue.js methods! So you guys give that a try and let me know how it goes. 

See you on the next post!