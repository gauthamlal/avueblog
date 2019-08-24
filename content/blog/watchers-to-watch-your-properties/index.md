---
title: Watchers, to Watch Your Properties!
date: "2019-08-24T11:30:00.000Z"
description: "To carry out a piece of logic when a particular property changes, we use watchers."
---

Last time we looked into Computed Property. Now as teased, let's diverge our attention to the other property to watch out for. Watchers!

Computed properties are great and useful but there are times when we need to just react to a particular property and you can do that using watchers. Another advantage that watchers have over computed is that they can be used to perform asynchronous operations. So you can perform your API calls in watchers when a particular property changes. Let's see a small example of watchers.

```html
<div id="app">
  <input type="text" v-model="value">
  <div>Square: {{ square }}</div>
</div>
```

```javascript
let app = new Vue({
  el: '#app',
  data: {
    value: 0,
    square: 0
  },
  watch: {
    value: function() {
      this.square = Math.pow(this.value, 2)
    }
  }
});
```

Using <code>v-model</code> for two way data-binding, we change the value of the <code>value</code> property from the input field. We then created a watcher for it by creating a function with name of the property we want to watch inside <code>watch</code>. And now whenever <code>value</code> changes, we calculate the square of it and assign it to the <code>square</code> property, which we then print on the screen.

So you can see how incredibly useful watchers are. You can write declarative code which you want to execute only when a particular property changes. It is also good for executing logic that applies to a different property when a change occurs in the property being watched.

Another useful tidbit is that your watcher functions can accept 2 parameters. The first is the new value and the other is the old value.

```javascript
watch: {
  value: function(newValue, oldValue) {
    console.log(newValue, oldValue)
  }
}
```

--- 

I mentioned how watchers are advantageous over computed in case of asynchronous operations. So let's simulate an asynchronous operation inside a watcher by using <code>setTimeout</code>.

```html
 <div id="app">
    <div>
        <p>Current Value: {{ value }}</p>
        <button v-on:click="value += 5">Add 5</button>
        <button v-on:click="value += 1">Add 1</button>
        <button v-on:click="reset()">Reset</button>
        <p>{{ result }}</p>
    </div>
</div>
```

So over here we have 3 buttons and we display two properties. The first two buttons are to add 5 and 1 to <code>value</code> property respectively while the third resets <code>value</code> to zero. <code>result</code> should show 'Not there yet' when value is not equal to 42 and it should show 'Done!' when it is. And <code>value</code> should be reset to zero, 5 seconds after the <code>result</code> changes. We can get this done by setting a watcher for <code>result</code>.

```javascript
let app = new Vue({
	el: '#app',
  data: {
  	value: 0,
    
  },
  methods: {
  	reset: function() {
    	this.value = 0;
    }
  },
  computed: {
  	result: function() {
    	return this.value === 42 ? 'Done!' : 'Not there yet'
    }
  },
  watch: {
    result: function() {
    	const self = this;
      setTimeout(function {
        if(self.value === 42) {
          self.value = 0;
        }
      }, 5000);
    }
  }
});
```

You can see that we are storing <code>this</code> in a variable before we access <code>value</code> inside setTimeout. This is because the Vue instance's <code>this</code> is not accessible within the function and we wouldn't be able to access <code>value</code> the way we usually do, <code>this.value</code>.

We watch for changes in <code>result</code> and when it changes we reset <code>value</code> to zero which in turn resets <code>result</code> to 'Not there yet'.

That's all for watchers. You could try and call dummy APIs inside them using [fetch()](https://developers.google.com/web/updates/2015/03/introduction-to-fetch). Here's a cool one, [Dog API](https://dog.ceo/dog-api/). Display images of dogs and change on the button click!

Catch you on the next post!