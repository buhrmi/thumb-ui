<script>
  import {Preload} from 'buhrmi'
</script>

<Preload url="https://i.imgur.com/E97i8c8.jpg" let:src>
  <img {src} alt="Great success">
  <div slot="fallback">Could not load image...</div>
</Preload>