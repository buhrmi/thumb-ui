<script>
import {onMount, getContext} from 'svelte'

const context = getContext('swipeable')

let i // my index

const progress = $context.progress
i = $context.numScreens
$context.numScreens++

// Calculate the css based on total Swipe progress.
// i is the screen index
// progress is a value from (0..covers.length)
$: style = `left: ${(i - $progress) * 100}%;`;

</script>

<div class="screen" {style} on:click={() => $context.jump(i)} >
  <slot />
</div> 

<style>
.screen {
  height: 100%;
  width: 100%;
  position: absolute;
}

</style>