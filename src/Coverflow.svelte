<script>
import Swipeable from './Swipeable.svelte'
import { onMount } from 'svelte'
import {fade} from 'svelte/transition'
import {quintOut} from 'svelte/easing'
	

export let covers = [
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

// Visual gap size between images
const gap = 9

// Rotation degree of images
const rotation = 90
let current = 3
let showdetails = true

// Calculate the css based on total Swipe progress.
// i is the cover index
// progress is a value from (0..covers.length)
function style(i, progress) {
  let offset = (i - progress)
  let blend = offset / 2 +0.5
  if (blend < 0) blend = 0
  if (blend > 1) blend = 1
  let rotateY = rotation - 2 * blend * rotation
  let transformOrigin = blend * 100
  return `left: ${offset * gap}vw; transform: rotateY(${rotateY}deg); transform-origin: ${transformOrigin}%`;
}
</script>

<div class="background">

  <h2>
    {covers[current].name}
  </h2>

  <div class="coverflow">
    <Swipeable
      speed="4"
      numStates={covers.length}
      bind:current
      let:jump
      let:progress>
 
  	  {#each covers as cover, i}
        <div class="cover" on:click={() => jump(i)} style={style(i, progress)}>
          <div class="img" style="background-image: url({cover.url})"/>
          <div class="img reflection" style="background-image:url({cover.url})"/>
        </div> 
      {/each}	
    </Swipeable>	
  </div>

  <div class="gradient" />
</div>


<style>
.background {
  background: #555562;
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  text-align: center;
  color: white;
  overflow: hidden;
  perspective: 800px;
}
.coverflow {
  margin: 0 auto;
  margin-top: 20px;
  display: inline-block;
  position: absolute;
  left: 50%;
  height: 48vw;
  max-height: 400px;
  width: 70vw;
  max-width: 600px;
  transform-style: preserve-3d;
  transform: translateX(-50%) translateZ(-100px);
  user-select: none;
}
.cover {
  height: 100%;
  width: 100%;
  position: absolute;
  box-shadow: 0 0 50px 0 rgba(0, 0, 0, 0.6);
}
.img {
  background-size: cover;
  height: 100%;
  width: 100%;
}
.img.reflection {
  filter: blur(10px);
  opacity: 0.2;
  transform: scaleY(-1);
  pointer-events: none;
}

.gradient {
  width: 100%;
  height: 100%;
  top: 50%;
  left: 0;
  position: absolute;
  background: linear-gradient(rgba(85,85,98,0) 0%, rgba(85,85,98,0.5) 20%,rgba(85,85,98,1) 50%);
  pointer-events: none;
}
h2 {
  margin-top: 40px;
  margin-bottom: 0px;
}
</style>
