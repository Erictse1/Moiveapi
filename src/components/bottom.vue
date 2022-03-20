<template>
  <div class="container">
    <font-awesome-icon @click="clickleft" icon="fa-solid fa-caret-left" />
    <p>{{ this.count }}</p>
    <font-awesome-icon @click="clickright" icon="fa-solid fa-caret-right" />
  </div>
</template>

<script>
import bus from './bus'
export default {
  data() {
    return {
      count: 1
    }
  },
  methods: {
    scrollToTop() {
      window.scrollTo(0, 0)
    },
    clickleft() {
      if (this.count > 1) this.count--
      bus.$emit('myevent', this.count)
      this.scrollToTop()
    },
    clickright() {
      if (this.count > 0) this.count++
      bus.$emit('myevent', this.count)
      this.scrollToTop()
    }
  },
  mounted() {
    bus.$on('myevent4', a => (this.count = a))
  }
}
</script>

<style lang="scss" scoped>
p {
  width: 30px;
  height: 30px;
  background: rgb(255, 217, 0);
  color: black;
  border-radius: 10px;
  display: flex;
  justify-content: center;
  align-items: center;
}
.container {
  background: black;
  max-width: 100%;
  padding: 15px;
  display: flex;
  justify-content: center;
  align-items: center;
  svg {
    padding: 10px;
    font-size: 40px;
    color: rgb(255, 217, 0);
  }
}
</style>
// cannot use this.route to push
