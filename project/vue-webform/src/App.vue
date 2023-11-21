<script>
import SignupForm from './components/SignupForm.vue'
export default {
    name: 'App',
    components: { SignupForm }
}
</script>

<template>
  <SignupForm />
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
