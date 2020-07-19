# Components

A collection of Svelte components.


## Preload

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

## Lazy

![Lazy Demo](https://github.com/buhrmi/components/blob/master/gifs/lazy.gif?raw=true)

[Demo](https://buhrmi.github.io/components/lazy)

Defers rendering of its content until the element scrolled into view. Takes [IntersectionObserver](https://developer.mozilla.org/en-US/docs/Web/API/IntersectionObserver/IntersectionObserver) options as props.

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


| Prop | Description | Example |
| --- | --- | --- |
| `root` | The element that is used as the viewport for checking visibility of the target. Must be the ancestor of the target. Defaults to the browser viewport if not specified or if null. | document.querySelector('#scrollArea') |
| `rootMargin` | Margin around the root. Can have values similar to the CSS margin property, e.g. "10px 20px 30px 40px" (top, right, bottom, left). The values can be percentages. This set of values serves to grow or shrink each side of the root element's bounding box before computing intersections. Defaults to all zeros. | "10px" |
| `threshold` | Either a single number or an array of numbers which indicate at what percentage of the target's visibility the observer's callback should be executed. If you only want to detect when visibility passes the 50% mark, you can use a value of 0.5. If you want the callback to run every time visibility passes another 25%, you would specify the array [0, 0.25, 0.5, 0.75, 1]. The default is 0 (meaning as soon as even one pixel is visible, the callback will be run). A value of 1.0 means that the threshold isn't considered passed until every pixel is visible. | 1.0 |


## Swipeable

Serves as a base to enable various touch-based interactions.

```html
<script>
  import { Swipeable } from 'buhrmi'
</script>

<Swipeable numStates="3" let:current let:progress>
  Currently in state #{current}, with a total swipe progress of {progress}
</Swipeable>
```

#### Props

| Prop | Description | Example |
| --- | --- | --- |
| `numStates` | The number of states (i.e. different screens) that the user can swipe to. | "4" |
| `speed` | How fast the progress changes relative to swipe speed | "4" |
| `direction` | Swipe direction. Horizontal (default) or vertical | "horizontal" |



## Coverflow

![Coverflow Demo](https://github.com/buhrmi/components/blob/master/gifs/coverflow.gif?raw=true)

[Demo](https://buhrmi.github.io/components/coverflow)

### Usage


```html
<script>
  import { Coverflow } from 'buhrmi'
</script>

<Coverflow {covers}/>
```

#### Props

| Prop | Description | Example |
| --- | --- | --- |
| `covers` | An array containing the url and name of each cover.|`[{url: ..., name: ...}]` |