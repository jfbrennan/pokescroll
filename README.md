# PokeScroll
Using the [pokeapi](https://pokeapi.co/docs/v2) to experiment with the Cache API and infinite scroll. 

The list of Pokemon are rendered from `CacheStorage`, otherwise the app fetches (and caches) pages of Pokemon as the user scrolls down. If there's any issues fetching, an internal retry mechanism will respond to those errors.

**One notable challenge:** Balancing buttery-smooth UX with DOM limits. The native `scrollIntoView` function is highly optimized by browsers for doing a targeted scroll, but it cannot work with old infinite scroll patterns like DOM recycling becuase the target element does not always exist. This means UX like scrolling to a specific item was always a large, difficult and error-prone implementation requiring debounced scroll events and manual calculation of placement of the element. That's no longer true with `IntersectionObserver` and `scrollIntoView` if using the right pattern. The primary performance concern nowadays is when DOM nodes are attached, which triggers a reflow. But once a list is built, there is very little concern for performance if you're leveraging native APIs, even for large scrolling lists. The browser can handle it.

One useful pattern for the most extreme cases (not applicable in this experiment) is to enforce an absolute height on each item in the list, continue to render the complete list, but for items not "intersecting" the content of those list items are not rendered. This can greatly reduce the size of the DOM when working with list of 1,000s of items each of which having a lot of content. The scroll UX continues to work nicely because each item still exists in the DOM and you can use an observer and `scrollIntoView`.

The UI is built with my [Mdash design system](http://m-docs.org).

Demo at https://jfbrennan.github.io/pokescroll/
