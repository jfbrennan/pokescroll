# PokeScroll
Using the [PokeAPI](https://pokeapi.co/docs/v2) to experiment with the Cache API and infinite scroll. 

The list of Pokemon are rendered from `CacheStorage`, otherwise the app fetches (and caches) pages of Pokemon as the user scrolls down. If there's any issues fetching, an internal retry mechanism will respond to those errors.

The UI is built with my [Mdash design system](http://m-docs.org).

Demo at https://jfbrennan.github.io/pokescroll/

## Infinite scroll and large lists
Balancing buttery-smooth UX and DOM limits should not be an issue nowadays if leveraging modern JavaScript APIs. 

The native `scrollIntoView` function is highly optimized by browsers for doing a targeted scroll, but it cannot work with old infinite scroll patterns like DOM recycling becuase the target element does not always exist. UX like scrolling to a specific item was always a large, difficult and error-prone implementation requiring debounced scroll events and manual calculation of placement of the element. That's no longer true with `IntersectionObserver` and `scrollIntoView` if following the right pattern. The primary performance concern today is when DOM nodes are first attached, which causes reflow. But once a list is built, there is very little concern for performance if you're leveraging native APIs, even for large scrolling lists. The browser can handle it.

One useful pattern for the most extreme cases (not applicable to this experiment) is to require an absolute height for each item in the list and continue to render the complete list. For elements in the list that are not "intersecting" their _content_ is not rendered. This will greatly reduce the size of the DOM when working with lists of 10,000+ of items that each have a lot of content. The scroll UX continues to work nicely when using this pattern because each item still gets an element in the DOM and so you can use an observer and `scrollIntoView`.
