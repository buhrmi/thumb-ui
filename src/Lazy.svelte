<script>
// This component defers rendering its slot until it has been scrolled into view

import { onMount } from 'svelte'
export let rootMargin='-100px'
export let root
export let threshold

let observer;
let node;
let intersected;

function onIntersect(entries){
  if (entries[0].isIntersecting) {
    intersected = true
    observer.unobserve(node)
    observer = null
  }
}  

onMount(function() {
  observer = new IntersectionObserver(onIntersect,{rootMargin, root, threshold});
  observer.observe(node);
  return {
    destroy() {
      observer.unobserve(node)
    }
  }
})
</script>

<div bind:this={node}></div>

{#if intersected}
  <slot />
{:else}
  <slot name="waiting" />
{/if}