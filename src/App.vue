<template>
  <div id="app">
    <Form />
  </div>
</template>

<script>
import Form from './components/Form.vue'

export default {
  name: 'App',
  components: {
    Form
  }
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Roboto:ital,wght@0,300;0,400;0,500;0,700;1,100&display=swap');

body{
  margin: 0;
  font-family: 'Roboto', sans-serif;
  overflow-x: hidden;
}

#app {
  width: 100vw;
  min-width: 18rem;
  padding: 2rem 0;
  background: #979797;
}

@media screen and (min-width: 1600px) {
  html {
    font-size: 120%;
  }
}

@media screen and (max-width: 900px){
    html {
      font-size: 90%;
    }
  }
</style>
