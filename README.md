# PokeScroll
Using the [pokeapi](https://pokeapi.co/docs/v2) to experiment with the Cache API and infinite scroll. The list of Pokemon are rendered from `CacheStorage` if available, otherwise fetches a large page of Pokemon using an internal retry mechanism to respond to errors.

The UI is built with my [Mdash design system](http://m-docs.org).

Demo at https://jfbrennan.github.io/pokescroll/
