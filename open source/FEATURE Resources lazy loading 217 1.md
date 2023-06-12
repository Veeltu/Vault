## Describe your changes

So I decide to use Intersection Observer for lazy loading on infinite scroll. I'm using the Intersection Observer configuration from the Svelte docs and creating easy-to-change variables to control the behavior. I think this solution is better than strict pagination.  
Thanks

##Related issue number/link

[#217](https://github.com/ClimateTown/knowledge-hub/issues/217)

[FEATURE] Resources lazy loading [#217](https://github.com/ClimateTown/knowledge-hub/issues/217)

Describe your suggested improvement  
Currently the resources page has all the resources loaded at once, which impacts the performance of the website. In future, this approach would also no longer be user friendly as the scrollbar would be small.

Implementing an infinite scroll/lazy loading approach where when the user nears the bottom of the page, new resources are loaded in would be great. Batches of ~20 resources at a time would suffice.

import from IntersectionObserver.svelte
```js
|// Constants for infinite scroll/lazy loading|
|||const DEFAULT_DISPLAY_LIMIT = 6;|
|||const SCROLL_THRESHOLD = 600;|
|||let displayedResourceLimit = DEFAULT_DISPLAY_LIMIT;|
|||let scrollPosition = 0;|
```
```js
|// Update the displayedResourceLimit based on the scroll position|
|||function updateDisplayLimit() {|
|||const { scrollTop, clientHeight, scrollHeight } = document.documentElement;|
|||const currentPosition = scrollTop + clientHeight;|
||||
|||if (currentPosition >= scrollHeight - SCROLL_THRESHOLD) {|
|||displayedResourceLimit += DEFAULT_DISPLAY_LIMIT;|
|||console.log("updateLimit");|
|||}|
|||}|
||||
|||// Event listener for scroll events and update limit|
|||function handleScroll() {|
|||scrollPosition = document.documentElement.scrollTop;|
||||
|||if (scrollPosition >= SCROLL_THRESHOLD) updateDisplayLimit();|
|||}|
||||
|||// Hook into component lifecycle events|
|||onMount(() => {|
|||window.addEventListener("scroll", handleScroll);|
|||});|
```

```js
|<IntersectionObserver let:intersecting top={200}>|
|||<div|
|||class="grid xl:grid-cols-3 md:grid-cols-2 sm:grid-cols-1 gap-x-4 gap-y-4 mt-3"|
|||>|
|||{#if intersecting}|
|||{#each displayedResources.slice(0, displayedResourceLimit) as resource}|
|||<ListItem {...resource} />|
|||{/each}|
|||{#if displayedResources.length === 0}|
|||<div>No resources here!</div>|
|||{/if}|
|||{/if}|
|||</div>|
|||</IntersectionObserver>|
```

in IntersectionObserver.svelte :
```js
<script>
import { onMount } from "svelte";
// Flag indicating whether the intersection should be observed only once
export let once = false;
// Margins for the intersection observer
export let top = 0;
export let bottom = 0;
export let left = 0;
export let right = 0;

let intersecting = false;
/**
* @type {Element}
*/
let container;

onMount(() => {
// Check if IntersectionObserver is supported by the browser
if (typeof IntersectionObserver !== "undefined") {
const rootMargin = `${bottom}px ${left}px ${top}px ${right}px`;

// Create the IntersectionObserver instance
const observer = new IntersectionObserver(
(entries) => {
intersecting = entries[0].isIntersecting;
if (intersecting && once) {
observer.unobserve(container);
}
},
{
rootMargin,
}
);
// Start observing the container element
observer.observe(container);
// Clean up the observer when the component is unmounted
return () => observer.unobserve(container);
}
// Fallback for browsers that do not support IntersectionObserver
function handler() {
const bcr = container.getBoundingClientRect();
intersecting =
bcr.bottom + bottom > 0 &&
bcr.right + right > 0 &&
bcr.top - top < window.innerHeight &&
bcr.left - left < window.innerWidth;

if (intersecting && once) {
window.removeEventListener("scroll", handler);
}
}

// Add scroll event listener to simulate intersection behavior
window.addEventListener("scroll", handler);
// Clean up the event listener when the component is unmounted
return () => window.removeEventListener("scroll", handler);
});
</script>
<div bind:this={container}>
<!-- Slot content that will be shown when intersecting is true -->
<slot {intersecting} />
</div>
<style>
div {
width: 100%;
height: 100%;
}
</style>
```

cool scroll top implementation
```js
|// Event listener for scroll events and update limit|
|||function handleScroll() {|
|||scrollPosition = document.documentElement.scrollTop;|
|||showButton = scrollPosition >= window.innerHeight * 2;|
|||if (scrollPosition >= SCROLL_THRESHOLD) updateDisplayLimit();|
|||}|
||||
|||// Hook into component lifecycle events|
|||onMount(() => {|
|||window.addEventListener("scroll", handleScroll);|
|||});|
||||
|||// for button|
|||function scrollToTop() {|
|||window.scrollTo({|
|||top: 0,|
|||behavior: "smooth",|
|||});|
```

## The best tutor about Intersection observer
https://www.smashingmagazine.com/2018/01/deferring-lazy-loading-intersection-observer-api/
typical observer regustration 
```js
/**
* Typical Observer's registration
*/
let observer = new YOUR-TYPE-OF-OBSERVER(function (entries) {
  // entries: Array of observed elements
  entries.forEach(entry => {
      // Here we can do something with each particular entry
  });
});

// Now we should tell our Observer what to observe
observer.observe(WHAT-TO-OBSERVE);

```
