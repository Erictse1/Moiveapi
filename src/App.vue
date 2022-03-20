<template>
  <div>
    <topbar :gen="genres.genres"></topbar>
    <Main></Main>
    <bottom></bottom>
  </div>
</template>

<script>
import topbar from './components/topbar.vue'
import Main from './components/main.vue'
import bottom from './components/bottom.vue'
import genres from './components/genres.json'
export default {
  components: { topbar, Main, bottom },
  data() {
    return { genres }
  }
}
</script>
<style lang="scss">
// #app {
//   font-family: Avenir, Helvetica, Arial, sans-serif;
//   -webkit-font-smoothing: antialiased;
//   -moz-osx-font-smoothing: grayscale;
//   text-align: center;
//   color: #2c3e50;
// }

body {
  background-color: #1b1b1b;
  // background-color: black;
  font-family: 'Poppins', sans-serif;
}

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

// .layout {
//   max-width: 840px;
//   margin: 0 auto;
//   padding-left: 20px;
//   padding-right: 20px;
// }
// .section {
//   margin-bottom: 30px;
// }
</style>
