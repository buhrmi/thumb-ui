# Thumb UI

A collection of Svelte components for thumb-driven web UIs.

This library is very experimental and I don't actually recommend using this for more than experimenting with Svelte.

![Example](https://github.com/buhrmi/components/blob/master/gifs/example.gif?raw=true)

## Table of Contents

- Components
  - Interactions
    - [Swipeable](#swipeable)
    - [Screen](#screen)
    - [Cover](#cover)
    - [Controls](#controls)
  - Utilities
    - [Preload](#preload)
    - [Lazy](#lazy-repl)
- Examples
  - [Carousel](#carousel-repl)
  - [Coverflow](#coverflow-repl)
  - [Custom Transitions](#custom-transitions-repl)
    

## \<Swipeable>

Serves as a base to enable various touch-based interactions.

```html
<script>
  import { Swipeable } from 'thumb-ui'
</script>

<Swipeable numScreens="3" let:current let:progress>
  Currently on screen #{current}, with a total swipe progress of {progress}
</Swipeable>
```

#### Props

| Prop | Description | Example |
| --- | --- | --- |
| `numScreens` | The number of screens that the user can swipe to. This is optional and is set automatically when using the component together with "pluggable" components like `Cover` | "4" |
| `speed` | How fast the progress changes relative to swipe speed | "4" |
| `direction` | Swipe direction. Horizontal (default) or vertical | "horizontal" |
| `current` | The index of the current screen | "3" |

## \<Screen>

A very simple component that plugs into a `Swipeable`. Allows the user to swipe between different screens.

[Example REPL](https://svelte.dev/repl/1af75faf851949a8a1a6978f144034e0?version=3.24.0)

## \<Cover>

A component that plugs into a `Swipeable` and presents its content in a Coverflow style.

![Coverflow Demo](https://github.com/buhrmi/components/blob/master/gifs/coverflow.gif?raw=true)

[Example REPL](https://svelte.dev/repl/156d5bb34eb0457ea1906998389a4e9f?version=3.24.0)

## \<Controls>

Plug it into a `Swipeable` to add navigation controls.

[Example REPL](https://svelte.dev/repl/1af75faf851949a8a1a6978f144034e0?version=3.24.0)

## \<Preload>

Defers rendering of its content until a resource has been loaded into the browser cache.
Provides a `fallback` slot to render if the resource can not be loaded.

### Usage

```html
<script>
  import {Preload} from 'thumb-ui'
</script>

<Preload url="https://i.imgur.com/E97i8c8.jpg" let:src>
  <img {src} alt="Great success">
  <div slot="fallback">Could not load image...</div>
</Preload>
```

## \<Lazy> ([REPL](https://svelte.dev/repl/9a37dc7103954474a32ec1ac3a587d26?version=3.24.0))

![Lazy Demo](https://github.com/buhrmi/components/blob/master/gifs/lazy.gif?raw=true)


Delays rendering of its content until the element scrolled into view. Takes [IntersectionObserver](https://developer.mozilla.org/en-US/docs/Web/API/IntersectionObserver/IntersectionObserver) options as props.

### Usage

```html
<script>
  import {Lazy} from 'thumb-ui'
  import {Preload} from 'thumb-ui'
  import {fly} from 'svelte/transition'
</script>

<Lazy rootMargin='-100px'>
  <Preload url="https://i.imgur.com/E97i8c8.jpg" let:src>
    <img {src} alt="Great success" in:fly={{x:60}}>
  </Preload>
</Lazy>
```

### Props

| Prop | Description  |
| --- | --- |
| `root` | The element that is used as the viewport for checking visibility of the target. Must be the ancestor of the target. Defaults to the browser viewport if not specified or if null. 
| `rootMargin` | Margin around the root. Can have values similar to the CSS margin property, e.g. "10px 20px 30px 40px" (top, right, bottom, left). The values can be percentages. This set of values serves to grow or shrink each side of the root element's bounding box before computing intersections. Defaults to all zeros. | 
| `threshold` | Either a single number or an array of numbers which indicate at what percentage of the target's visibility the observer's callback should be executed. If you only want to detect when visibility passes the 50% mark, you can use a value of 0.5. If you want the callback to run every time visibility passes another 25%, you would specify the array [0, 0.25, 0.5, 0.75, 1]. The default is 0 (meaning as soon as even one pixel is visible, the callback will be run). A value of 1.0 means that the threshold isn't considered passed until every pixel is visible. 

## Examples

### Carousel ([REPL](https://svelte.dev/repl/1af75faf851949a8a1a6978f144034e0?version=3.24.0))

Demonstrates how you can use the `Swipeable`, `Screen`, `Preload` and `Controls` components to build a cool image carousel.

![Carousel Demo](https://github.com/buhrmi/components/blob/master/gifs/carousel.gif?raw=true)

### Coverflow [REPL](https://svelte.dev/repl/156d5bb34eb0457ea1906998389a4e9f?version=3.24.0)

Demonstrates how you can build a Coverflow UI using `Swipeable` and `Cover`.

![Coverflow Demo](https://github.com/buhrmi/components/blob/master/gifs/coverflow.gif?raw=true)

### Custom Transitions [REPL](https://svelte.dev/repl/9116699f10ac42668e7b58d120c4bc8c?version=3.18.1)

Demonstrates using only the Swipeable component and its "raw" bindings to create custom transitions.

![Example](https://github.com/buhrmi/components/blob/master/gifs/example.gif?raw=true)
