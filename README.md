# Svelte Components

A collection of Svelte components.

## Swipeable

Enables various touch-based interactions.

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
