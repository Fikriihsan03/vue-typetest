<template>
  <div class="progressbar" :style="{ width:second/30*100+'%', fontSize: fontSize + 'px' }">
  </div>
</template>
<script>
export default{
  props:{
    second:Number
  }
}
</script>
<style>
/* Sets the container's height and width */
.root {
  height: 70px;
  width: 70px;
  position: relative;
}
.progressbar{
  height: 1px;
  width: 100%;
  background-color: aqua;
}
/* Removes SVG styling that would hide the time label */
.circle {
  fill: none;
  stroke: none;
}

/* The SVG path that displays the timer's progress */
.time-elapsed-path {
  stroke-width: 7px;
  stroke: #424242;
}
</style>