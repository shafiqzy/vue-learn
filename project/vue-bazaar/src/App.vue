<script>
import bazaarInsert from './components/bazaarInsert.vue'

export default {
    name: 'App',
    components: { bazaarInsert }
}
</script>

<template>
  <bazaarInsert/>

</template>

<style>
#app{
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align:center;
  color: #2c3e50;
  margin-top: 60x;
}
body{
  margin: 0;
  background: #eee;
}
</style>
