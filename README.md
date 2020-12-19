# Thumb UI

A collection of Svelte components for thumb-driven web UIs.

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

## \<Screen>

A very simple component that plugs into a `Swipeable`. Allows the user to swipe between different screens.

S
