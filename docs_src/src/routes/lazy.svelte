<script>
import {Lazy} from 'buhrmi'
import {Preload} from 'buhrmi'
import {fly} from 'svelte/transition'

const urls = [
  'https://i.imgur.com/WSNVjAp.jpg',
  'https://i.imgur.com/ktLr47i.jpg',
  'https://i.imgur.com/IBPaYOH.jpg',
  'https://i.imgur.com/E97i8c8.jpg',
  'https://i.imgur.com/eurkXGH.jpg',
  'https://i.imgur.com/1BdAJno.jpg',
  'https://i.imgur.com/0AZOG1D.jpg',
  'https://i.imgur.com/qlgU0n9.jpg',
  'https://i.imgur.com/Qol6aNw.jpg'
]
</script>

{#each urls as url}
  <div class="section">
    <Lazy>
      <Preload {url} let:src>
        <img {src} alt="Great success" in:fly={{x:60}}>
      </Preload>
    </Lazy>
  </div>
{/each}

<style>
.section {
  overflow: hidden;
  height: 60vw;
  max-height: 400px;
}
img {
  width: 100%;
}
</style>