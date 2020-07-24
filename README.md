# Components

A collection of Svelte components for thumb-driven web UIs.

The goal of this component library is to make it easy to create mind-blowing user interfaces for the mobile web.

## Table of Contents

- Components
  - Interactions
    - [Swipeable](#swipeable)
    - [Screen](#screen-repl)
    - [Cover](#cover-repl)
    - [Controls](#controls-repl)
  - Utilities
    - [Preload](#preload)
    - [Lazy](#lazy-repl)
- Examples
  - [Carousel](#carousel-repl)
  - [Coverflow](#coverflow-repl)
    

## \<Swipeable>

Serves as a base to enable various touch-based interactions.

```html
<script>
  import { Swipeable } from 'buhrmi'
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



## \<Cover> [REPL](https://svelte.dev/repl/156d5bb34eb0457ea1906998389a4e9f?version=3.24.0)

A component that plugs into a `Swipeable` and presents its content in a Coverflow style.

![Coverflow Demo](https://github.com/buhrmi/components/blob/master/gifs/coverflow.gif?raw=true)


### Usage


```html
<script>
  import {Swipeable, Cover} from 'buhrmi'
  let covers = [
    {url: 'https://i.imgur.com/WSNVjAp.jpg', name: 'Lamborghini Veneno'},
    {url: 'https://i.imgur.com/ktLr47i.jpg', name: 'Zenvo TS1'},
    {url: 'https://i.imgur.com/IBPaYOH.jpg', name: 'McLaren P1 LM'},
    {url: 'https://i.imgur.com/E97i8c8.jpg', name: 'LaFerrari FXX K'}
  ]
  let current = 3
</script>

<div class="container">
  <Swipeable speed="3" bind:current>
    {#each covers as cover}
      <Cover>
        <div class="img" style="background-image: url({cover.url})" />
        <div class="img reflection" style="background-image:url({cover.url})" /> 
      </Cover>
    {/each}
  </Swipeable>
</div>

<style>
.container {
  margin: 30px auto;
  position: relative;
  height: 280px;
  width: 360px;
  perspective: 800px;
  transform-style: preserve-3d;
  user-select: none;
}
.img {
  background-size: cover;
  background-position: center;
  height: 100%;
  width: 100%;
  box-shadow: 0 0 50px 0 rgba(0, 0, 0, 0.6);
}
.img.reflection {
  filter: blur(10px);
  opacity: 0.2;
  transform: scaleY(-1);
  pointer-events: none;
}
</style>
```

## \<Controls> [REPL](https://svelte.dev/repl/21e3078f26f94911be1d91452748b3a8?version=3.24.0)

Adds navigation controls when plugged into a `Swipeable`.

### Usage

```html
  <Swipeable>
    ....

    <Controls />
  </Swipeable>
```

## \<Carousel> ([REPL](https://svelte.dev/repl/1af75faf851949a8a1a6978f144034e0?version=3.24.0))

A simple image carousel 

![Lazy Demo](https://github.com/buhrmi/components/blob/master/gifs/carousel.gif?raw=true)

### Usage

```html
<script>
import {Carousel} from 'buhrmi'
const images = [
  'https://i.imgur.com/WSNVjAp.jpg',
  'https://i.imgur.com/ktLr47i.jpg',
  'https://i.imgur.com/IBPaYOH.jpg',
  'https://i.imgur.com/E97i8c8.jpg',
]

</script>

<main>
  <Carousel {images} />
</main>

<style>
main {
  max-width: 600px;
}
</style>
```

## \<Preload>

Defers rendering of its content until a resource has been loaded into the browser cache.
Provides a `fallback` slot to render if the resource can not be loaded.

### Usage

```html
<script>
  import {Preload} from 'buhrmi'
</script>

<Preload url="https://i.imgur.com/E97i8c8.jpg" let:src>
  <img {src} alt="Great success">
  <div slot="fallback">Could not load image...</div>
</Preload>
```

## \<Lazy> ([REPL](https://svelte.dev/repl/9a37dc7103954474a32ec1ac3a587d26?version=3.24.0))

![Lazy Demo](https://github.com/buhrmi/components/blob/master/gifs/lazy.gif?raw=true)


Defers rendering of its content until the element scrolled into view. Takes [IntersectionObserver](https://developer.mozilla.org/en-US/docs/Web/API/IntersectionObserver/IntersectionObserver) options as props.

### Usage

```html
<script>
  import {Lazy} from 'buhrmi'
  import {Preload} from 'buhrmi'
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