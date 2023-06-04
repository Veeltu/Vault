The Intersection Observer API provides a way to:
- asynchronously observe changes 
- in the intersection of a target element 
- with an ancestor element 
- or with a top-level document's [viewport](https://developer.mozilla.org/en-US/docs/Glossary/Viewport).
- https://developer.mozilla.org/en-US/docs/Web/API/Intersection_Observer_API

In short, it enables you to detect the visibility of an element, i.e. if it’s in the current viewport, and also the relative visibility of two elements in relationship to each other.

# Use Cases

- Lazy loading of images.
- Infinite scrolls.
- Prefetching of links when they appear on the screen (Gatsby does this).
- To detect whether an ad was viewed or not (more tracking).
- To determine whether a user has read an article and to what extent (think medium view vs. read stats).
- To run costly renderings and animations only when they are visible on the screen.

At the core of the Intersection Observer API are the following two lines:

var observer = new IntersectionObserver(callback, options);  
observer.observe(target);

1. First, you create an `Observer` with some `options`.
2. Then, you ask the `Observer` to start `observing` a `target`.
3. When the desired `intersection` happens, your `callback` function is called.

# The Options

This was the tricky part to understand. Before going through the settings in options, you should have a firm grasp on the following:

**Intersection Observer API** lets you do something in the **callback function** when it **observes** an **intersection** (beyond a certain **threshold**) between the **root** element and the **target** element.

1. Think of `root` as the outer rectangle, or the rectangle within which you want to observe for an intersection.
2. `target` is the element which you are watching.
3. `threshold` gives you the extent to which the overlap should occur.
4. `rootMargin` is the margin applied to the root before the extent of the intersection is calculated.

# Rules of Thumb

1. The API is asynchronous, so use the `callback` function to do something when the intersection happens.
2. The `root` element can be decided using the CSS selector.
3. If you specify `root: document.querySelector(‘null’)`, the current viewport of the user will be the `root` element.
4. Play around with `threshold` and `rootMargin` to get the exact behavior you are expecting.

This is pretty much the core concept in Intersection Observer API. For further reading, see [MDN’s documentation](https://developer.mozilla.org/en-US/docs/Web/API/Intersection_Observer_API).
===========================================================================
simple project : 

app.js 
```js 
//instalation for observer
const observer = new IntersectionObserver((entries) => {
entries.forEach((entry) => {
console.log(entry)
//if its "obserwowany" do this
if (entry.isIntersecting) {
entry.target.classList.add("show")
}
//remove "show" when not "obserwowany"
// else {
// entry.target.classList.remove("show")
// }
})
})
const hiddenElements = document.querySelectorAll('.hidden')
//obserwuje te elementy
hiddenElements.forEach((el) => observer.observe(el));
```
style.css
```css
.hidden {
opacity: 0;
transition: all 1s ease-in-out;
filter: blur(5x);
transform: translateX(-100%);
}

.show {
opacity: 1;
transition: all 1s ease-in-out;
transform: translateX(0);
}
```

