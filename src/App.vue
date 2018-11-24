<template>
  <div id="app">
    <vapelator/>
  </div>
</template>

<script>
import Vapelator from './components/Vapelator.vue'

export default {
  components: {
    Vapelator
  }
}
</script>

<style>

@font-face {
  font-family: 'gilroyextrabold';
  src: url('./assets/fonts/Gilroy-ExtraBold.otf') format('opentype');
  font-weight: bold;
  font-style: normal;
  }

body{
  background: linear-gradient( rgba(255, 221, 0, 0.8), rgba(255, 221, 0, 0.8)),
    url('./assets/sky.jpg') 0 0 no-repeat fixed;
  background-size:  cover;
  background-position: center;
}

#app {
  font-family: 'gilroyextrabold', Helvetica, Arial, sans-serif;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;

}


</style>
