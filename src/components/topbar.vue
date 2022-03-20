<template>
  <header>
    <form id="form" v-on:submit.prevent="climethod">
      <input
        type="text"
        placeholder="Search"
        id="search"
        class="search"
        ref="userInput"
      />
      <label for="moive"></label>
    </form>
    <select style="width: 200px" @change="optionMid($event.target.value)">
      <option v-for="(a, index) in gen" :value="a.id" :key="index">
        {{ a.name }}
      </option>
    </select>
  </header>
</template>

<script>
import bus from './bus'

export default {
  props: {
    gen: {
      type: Array,
      required: true,
      default: function () {
        return []
      }
    }
  },
  data() {
    return {
      userInput: '',
      value: ''
    }
  },
  methods: {
    climethod() {
      // console.log(this.$refs.userInput.value)
      // this.$refs.userInput.abc(2)
      bus.$emit('myevent2', this.$refs.userInput.value)
    },
    optionMid(e) {
      bus.$emit('myevent3', e)
    }
  }
}
</script>

<style lang="scss" scoped>
label {
  padding-left: 100px;
}
select {
  background: rgb(255, 217, 0);
  height: 38px;
  color: #1b1b1b;
  font-weight: 500;
  font-size: 13px;
}

header {
  background: linear-gradient(0deg, transparent, rgba(0, 0, 0, 0.7) 50%);
  // background-color: #373b69;

  padding: 20px 0 20px 60px;
  display: flex;
  justify-content: center;
  align-items: center;
}
input {
  text-align: left;
}
.search {
  padding-left: 10px;
  width: 360px;
  height: 45px;
  border: 2px solid #22254b;
  border-radius: 10px;
  background-color: transparent;
  font-size: 1rem;
  color: #fff;
  font-family: inherit;
}
.search:focus {
  outline: 0;
  background-color: #1b1b1b;
}
.search:focus::placeholder {
  color: #fff;
  //   padding-left: 50px;
}
.search::placeholder {
  color: antiquewhite;
}
</style>
//
//https://api.themoviedb.org/3/discover/movie?language=zh-hk&api_key=4e52779f06db596b6259e03286a04184&page=1&with_genres=35
