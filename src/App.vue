<template>
  <signupForm />
</template>

<script>

import signupForm from './components/signupForm.vue'

export default {
  name: 'App',
  components: { signupForm }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

body {
    background: repeating-radial-gradient(tomato, indigo 10%, lightgreen 15%);
    border: 30px double black;
}
</style>
