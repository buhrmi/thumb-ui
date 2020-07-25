<script>
import { onMount, tick, setContext } from 'svelte'
import { tweened } from 'svelte/motion'
import { cubicOut } from 'svelte/easing'
import { writable } from 'svelte/store'

export let current = 0
export let direction = 'horizontal'
export let numScreens = 0
export let speed = 1

let el

let dragging = false
let lastPosition
let draggedPixels = 0
let draggedBack
let jumpEnabled = true
let clientHeight
let clientWidth

export const progress = tweened(current, {
	duration: 400,
	easing: cubicOut
})

export const context = writable({
	jump,
	next,
	prev,
	progress,
	numScreens
})
setContext('swipeable', context)

$: current = Math.floor($progress+0.5)
$: positionField = direction == 'vertical' ? 'pageY' : 'pageX'
$: maxSlideIndex = $context.numScreens - 1
$: size = direction == 'vertical' ? clientHeight : clientWidth

onMount(function() {
	draggedPixels = current * (direction == 'vertical' ? clientHeight : clientWidth)
})
	
function startMove(startPosition) {
	draggedPixels = $progress * size
	dragging = true
	lastPosition = startPosition;
}


export function next(e) {
	if (e) e.stopPropagation()
	if (dragging) return
	draggedPixels += size
  $progress = (draggedPixels / size) || 0
	// if (draggedPixels < maxSlideIndex * size) draggedPixels = 0
}

export function prev(e) {
	if (e) e.stopPropagation()
	if (dragging) return
	draggedPixels -= size
	$progress = (draggedPixels / size) || 0
	// if (draggedPixels > 0) draggedPixels = 0
}


function move(position) {
	if (!dragging) return
	let delta = position - lastPosition
	
	lastPosition = position
	draggedPixels -= delta * speed
	if (draggedPixels < 0) draggedPixels = 0
	if (draggedPixels > maxSlideIndex * size) draggedPixels = maxSlideIndex * size
	draggedBack = delta < 0
	jumpEnabled = false
	$progress = (draggedPixels / size) || 0

}

function stopMove() {
	if (draggedBack) draggedPixels = Math.ceil(draggedPixels / size) * size
	else draggedPixels = Math.floor(draggedPixels / size) * size
	dragging = false
	stopTimeout = null
	clearTimeout(stopTimeout)
	$progress = (draggedPixels / size) || 0
	// when release the mouse, the click event gets fired, calling the jump function, undoing the drag.
	// disable jump for one tick.
	setTimeout((() => jumpEnabled = true), 10)
	

	// clearTimeout(nextSlideTimeout)
	// nextSlideTimeout = setTimeout(nextSlide, 10000)
}

function mousedown(e) {
	//e.preventDefault()
	startMove(e[positionField])
}

function mouseup(e) {
	stopMove()
}

function mousemove(e) {
	e.preventDefault()
	if (stopTimeout) return // we just used the wheel
	move(e[positionField])
}

function touchstart(e) {
	// e.preventDefault()
	startMove(e.changedTouches[0][positionField])
}

function touchend(e) {
	stopMove()
}
	
function pointercancel(e) {
	dragging = false
}
	
export function jump(i){
	if (!jumpEnabled) return
	draggedPixels = i * size
	$progress = i
}

function click(e) {
  e.stopPropagation()
}
	
function touchmove(e) {	
	//e.preventDefault()
	move(e.changedTouches[0][positionField])
}
	
let stopTimeout
function wheel(e) {
	let delta = direction == 'vertical' ? -e.deltaY : -e.deltaX
	if (delta != 0) e.preventDefault()
	startMove(0)
	move(delta)
	clearTimeout(stopTimeout)
	stopTimeout = setTimeout(stopMove, 100)
}

</script>

<div bind:clientWidth 
		 bind:clientHeight
		 on:pointercancel={pointercancel}
		 on:touchstart={touchstart} 
		 on:touchmove={touchmove} 
		 on:touchend={touchend} 
		 on:mousedown={mousedown} 
		 on:mousemove={mousemove} 
		 on:mouseup={mouseup} 
		 on:wheel={wheel}
		 on:click={click}
		 bind:this={el} 
		 class="swipeable {direction}">
	<slot {current} {jump} progress={$progress}></slot>
</div>

<style>
.swipeable {
	width: 100%;
	height: 100%;
}
.horizontal {
	touch-action: pan-y;
}
.vertical {
	touch-action: pan-x;
}
</style>