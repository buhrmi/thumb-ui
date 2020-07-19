<script context="module">
  const preloaded = {}
</script>

<script>
function preload(src) {
  if (preloaded[src]) return Promise.resolve(src)
  if (!src) src = fallback
  return new Promise(function(resolve, reject) {
    let img = new Image()
    img.onload = () => {
      preloaded[src] = true
      resolve(src)
    }
    img.onerror = reject
    img.src = src
  })
}
export let url
export let fallback
</script>

{#await preload(url, fallback) then src}
  <slot {src} />
{:catch error}
  <slot name="fallback" />
{/await}