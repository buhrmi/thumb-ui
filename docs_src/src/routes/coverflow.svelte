<script>
  import {Swipeable, Cover} from 'buhrmi'
  let covers = [
    {url: 'https://i.imgur.com/WSNVjAp.jpg', name: 'Lamborghini Veneno'},
    {url: 'https://i.imgur.com/ktLr47i.jpg', name: 'Zenvo TS1'},
    {url: 'https://i.imgur.com/IBPaYOH.jpg', name: 'McLaren P1 LM'},
    {url: 'https://i.imgur.com/E97i8c8.jpg', name: 'LaFerrari FXX K'},
    {url: 'https://i.imgur.com/eurkXGH.jpg', name: 'Bugatti Chiron'},
    {url: 'https://i.imgur.com/1BdAJno.jpg', name: 'Lamborghini Centenario'},
    {url: 'https://i.imgur.com/0AZOG1D.jpg', name: 'Aston Martin One-77'},
    {url: 'https://i.imgur.com/qlgU0n9.jpg', name: 'Pagani Huayra'},
    {url: 'https://i.imgur.com/Qol6aNw.jpg', name: 'W Motors Lykan Hypersport'}
  ]
  let current = 3
</script>

<div class="container">
  <Swipeable speed="3" bind:current>
    {#each covers as cover}
      <Cover>
          <div class="img" style="background-image: url({cover.url})"/>
          <div class="img reflection" style="background-image:url({cover.url})"/> 
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