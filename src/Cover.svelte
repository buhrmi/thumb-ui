<script>
import {onMount, getContext} from 'svelte'

// Visual gap size between images
export let gap = 9

// Rotation degree of images
export let rotation = 90

const context = getContext('swipeable')

let i // my index
let style
const progress = $context.progress
i = $context.numScreens
$context.numScreens++

// Calculate the css based on total Swipe progress.
// i is the cover index
// progress is a value from (0..covers.length)
$: {
  let offset = (i - $progress)
  let blend = offset / 2 +0.5
  if (blend < 0) blend = 0
  if (blend > 1) blend = 1
  let rotateY = rotation - 2 * blend * rotation
  let transformOrigin = blend * 100
  style = `left: ${offset * gap}vw; transform: rotateY(${rotateY}deg); transform-origin: ${transformOrigin}%`;
}

</script>

<div class="cover" {style} on:click={() => $context.jump(i)} >
  <slot />
</div> 

<style>
.cover {
  height: 100%;
  width: 100%;
  position: absolute;
}

</style>