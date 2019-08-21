---
title: Computed Properties, What Are They?
date: "2019-08-21T22:00:00.000Z"
description: "While methods are useful, we have an alternative that can be more efficient. Computed Properties."
---

Let's go back to the [very first blog post](https://avueblog.netlify.com/hello-world/) where we talked about templates. Another useful thing about templates is that you can write simple JavaScript expressions in them.

```html
<div>{{ count * 10 }}</div>
```

While this is extremely useful, they are limited to single expressions. And when they tend to get long, the code gets bloated and can be tough to read. And in case you need to repeat the same at multiple places, it leads to repetitive code.

In comes the <code>computed</code> property to save the day. Let's look at an example.

```html
<div id="app">{{ getFullName }}</div>
```

```javascript
let app = new Vue({
  el: '#app',
  data: {
    firstName: 'Light',
    lastName: 'Yagami',
  },
  computed: {
    getFullName: function() {
      return this.firstName + ' ' + this.lastName;
    }
  }
});
```

And we get the full name printed! Now whenever you change the value of the data properties being used inside the <code>getFullName</code> computed property, it returns a new full name. So if you go ahead and make a change like <code>app.lastName = "Kira"</code>, a new full name 'Light Kira' gets printed!

## Computed vs Methods

You must have noticed we could've received the same result by using methods.

To begin with, although computed properties are functions at the end of the day, we didn't have to call them by <code>getFullName()</code>, like methods. We can call them the same way we do with data properties.

Although the end results are the same, the way computed and method properties get there are different. **Computed properties are cached**. What it means is that the result of a computed property is internally cached and is re-evaluated only when a reactive source gets updated. This means as long as <code>firstName</code> and <code>lastName</code> remains the same, subsequent calls to <code>getFullName</code> does not cause a re-execution of the function and in turn returns the previously calculated cached result.

It is also important to note that the dependant property has to be reactive. Hence the following will not cause a re-render.

```javascript
computed: {
  nowDate: function() {
    return Date.now();
  }
}
```

It will render once and will not update on subsequent re-renders.

A huge upside of using computed over methods is the caching. In a case where we have a huge computed property with a lot of computations, execution of computed property on every re-render even when the data source hasn't changed can be expensive. Computed property lets us skip this by caching the result and returning the same till a re-execution is needed.

But that's not all! In the next post, we have another property to look out for. Or should I say, watch out for?

Until next time, bye!