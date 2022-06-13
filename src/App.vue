<template>
  <HelloWorld/>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue"
export default {
  components: { HelloWorld }
}
</script>

<style>
:root{
  --scheme-background: white;
  --scheme-font-color: black;
}

html { 
  background-color: var(--scheme-background);
  color: var(--scheme-font-color);
  transition: background-color .4s;

  touch-action: none;
  -webkit-overflow-scrolling: touch; /* enables “momentum” (smooth) scrolling */

  /* Nice Font */
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

body {
  width:100%;
  height:100%;
  overflow: auto;
  position: relative;
  overflow-x:hidden!important;
  margin:0 auto;
}
</style>
