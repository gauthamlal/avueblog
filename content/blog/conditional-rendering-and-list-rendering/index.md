---
title: Conditional Rendering and List Rendering in Vue.js
date: "2019-08-31T21:45:00.000Z"
description: "Looking deeper into the directives that help us render based on conditions and lists."
---

In my post on [directives](https://avueblog.netlify.com/fantastic-directives-and-how-to-use-them/) I talked about <code>v-if</code> and <code>v-for</code>. Today let's take a deeper look into both.

## <code>v-if</code>

We can use this directive to conditionally render a block. Whether the block will get rendered depends on the [truthiness](https://developer.mozilla.org/en-US/docs/Glossary/Truthy) of the expression in the directive. <code>v-if</code> removes the block from the DOM and hence won't be rendered.

```html
<p v-if="isTrue">You can see me!</p>
```

#### `v-else`

You can use <code>v-else</code> directive for rendering an alternate block when the <code>v-if</code> condition is not true.

```html
<p v-if="isTrue">You can see me!</p>
<p v-else>Now you don't!</p>
```

#### `v-else-if`

There is a <code>v-else-if</code> directive as well, which can be chained multiple times and it can serve an 'else-if' block.

```html
<div v-if="number === 1">
  One
</div>
<div v-else-if="number === 2">
  Two
</div>
<div v-else-if="number === 3">
  Three
</div>
<div v-else>
  Not One or Two or Three
</div>
```

One thing to keep in mind while using <code>v-else</code> and <code>v-else-if</code> is that they should immediately follow a <code>v-if</code> or a <code>v-else-if</code>.

#### `v-if` on `<template>`

Now there might come situations where we have to render multiple blocks based on a condition. We can use `v-if` on `<template>` in that case to create an invisible wrapper. The output that gets rendered will not include the `<template>` element. This can also help us avoid the unwanted use of `<div>` tags.

```html
<template v-if="showUser">
  <h1>Name</h1>
  <p>Username</p>
  <p>Title</p>
</template>
```
#### `v-show`

We have another directive for conditionally displaying elements called `v-show`. We can use it similarly to `v-if`.

```html
<p v-show="isShow">You can see me!</p>
```

The difference is that the block will get always rendered but just hides it when the expression is falsy. It toggles the `display` CSS property of the element. You can view this in the 'Elements' tab of your browser's developer tools.

```html
<p v-show="isShow">You can see me!</p>
<button v-on:click="isShow = !isShow"></button>
```

The above toggles the value of `isShow` on the button click. In the developer console, you can see that a style `display: none` is being added to the `<p>` element.

A thing to keep in mind is that `v-else` and `v-else-if` cannot be used with `v-show`. `v-show` also does not support `<template>` element.

---

## `v-for`

`v-for` directive lets us render a list of items in an array or an object. The required syntax is `item in items` where `item` is the element currently being iterated on from the `items` array or object.

#### `v-for` on arrays

```html
<ul>
  <li v-for="ingredient in ingredients">{{ ingredient }}</li>
</ul>
```

```javascript
data: {
  	ingredients: ['meat', 'fruit', 'cookies']
}
```

The above `v-for` will render an unordered list with the array elements in `ingredients` as list items.

<ul>
  <li>meat</li>
  <li>fruit</li>
  <li>cookies</li>
</ul>

`v-for` also allows, you to have an optional second parameter, the index of the item.

```html
<ul>
  <li v-for="(ingredient, index) in ingredients">{{ ingredient }} - {{ index }}</li>
</ul>
```

#### `v-for` on objects

Similar to iterating through the elements of an array, `v-for` can be used to iterate through the properties of an object.

```html
<ul>
  <li v-for="object in myObject">{{ object }}</li>
</ul>
```

```javascript
data: {
  myObject: {
    title: 'Lord of the Rings',
    author: 'J.R.R. Tolkien',
    books: '3'
  }
}
```

Result:

<ul>
  <li>Lord of the Rings</li>
  <li>J.R.R. Tolkien</li>
  <li>3</li>
</ul>

You can also provide a second and a third argument to get the property name (or key) and index.

```html
<ul>
  <li v-for="(object, k, i) in myObject">{{ k }}: {{ object }} - {{ i }}</li>
</ul>
```

<ul>
  <li>title: Lord of the Rings - 0</li>
  <li>author: J.R.R. Tolkien - 1</li>
  <li>books: 3 - 2</li>
</ul>

---

Similar to `v-if`, `v-if` can also be used with `<template>` to render a block multiple times.

`v-if` can also be used with `v-for` to check whether the block should be rendered for each element based on a condition. `v-if` can be used on the wrapper element of `v-for` to skip the loop.

`v-for` can be used to render a block a given number of times by passing it an integer.

```html
<ul>
  <li v-for="n in 10">{{ n }} </li>
</ul>
```

Result:

1 2 3 4 5 6 7 8 9 10

#### Providing a `key` to `v-for`

Vue uses an "in-place patch" strategy where if the order of the items changes, Vue will patch element in place to match the new order instead of reordering the items. While this is efficient, in complex cases it could cause hindrance.

To let Vue track each item, we can provide a unique `key` to each element. This lets Vue identify the elements and track changes and then reuse and reorder them when necessary. This essentially avoids the re-render of the entire loop.

You can provide `key` with the help of `v-bind`.

```html
<li v-for="(ingredient, i) in ingredients" :key="ingredient">{{ ingredient }} ({{ i }})</li>
```

---

So Vue makes our life easier by providing us `v-for` and `v-if`. They are flexible and can even be used together to solve routine use cases easily.