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

---

Now that we have got our heads around Vue methods, it's time for a challenge. Remember that we set up a counter that increments on every button click in the last [post](https://avueblog.netlify.com/fantastic-directives-and-how-to-use-them/)? Now you could try to do that with Vue.js methods! So you guys give that a try and let me know how it goes. 

See you on the next post!