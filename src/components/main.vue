<template>
  <div class="container">
    <ul>
      <li v-for="a in list" :key="a.id">
        <div class="overviewandimage">
          <img :src="`https://image.tmdb.org/t/p/w500${a.poster_path}`" />
          <div class="overinover">
            <h3>Overview</h3>
            <p class="overview">{{ a.overview }}</p>
          </div>
        </div>
        <div class="titleandvote">
          <p class="title">{{ a.title }}</p>
          <p class="vote">{{ a.vote_average }}</p>
        </div>
      </li>
    </ul>
  </div>
</template>
<script>
import axios from 'axios'
import Vue from 'vue'
import bus from './bus'
export default {
  data() {
    return {
      list: [],
      pichttps: 'https://image.tmdb.org/t/p/w500',
      counter: 1,
      genres: ''
    }
  },
  methods: {},
  mounted() {
    axios({
      url: `https://api.themoviedb.org/3/discover/movie?language=zh-hk&api_key=4e52779f06db596b6259e03286a04184&page=${this.counter}&with_genres=${this.genres}`
    }).then(a => {
      console.log(a.data.results)
      this.list = a.data.results
    })
  } /* eslint-disable */,
  updated() {
    bus.$on('myevent', data => {
      this.counter = data
      axios({
        url: `https://api.themoviedb.org/3/discover/movie?language=zh-hk&api_key=4e52779f06db596b6259e03286a04184&page=${this.counter}&with_genres=${this.genres}`
      }).then(a => {
        this.list = a.data.results
      })
    })
    bus.$on('myevent2', data => {
      axios({
        url: `https://api.themoviedb.org/3/search/movie?language=zh-hk&api_key=1cf50e6248dc270629e802686245c2c8&query=${data}`
      }).then(a => {
        this.list = a.data.results
      })
    })
    bus.$on('myevent3', data => {
      this.genres = data
      this.counter = 1
      bus.$emit('myevent4', 1)

      axios({
        url: `https://api.themoviedb.org/3/discover/movie?language=zh-hk&api_key=4e52779f06db596b6259e03286a04184&page=1&with_genres=${this.genres}`
      }).then(a => {
        this.list = a.data.results
      })
    })
    // bus.$on('myevent', data => (this.counter = data))
    // axios({
    //   url: `https://api.themoviedb.org/3/discover/movie?language=zh-hk&api_key=4e52779f06db596b6259e03286a04184&page=${this.counter}`
    // }).then(a => {
    //   this.list = a.data.results
    // })
    //function 1
    // why keep looping?only one in update
    //https://api.themoviedb.org/3/discover/movie?language=zh-hk&api_key=4e52779f06db596b6259e03286a04184&page=1&with_genres=35
  }
}
</script>

<style lang="scss" scoped>
.container {
  max-width: 1400px;
  margin: 0 auto;
  .overview {
    width: 350px;
    overflow: auto;
    height: 200px;
  }
  .overviewandimage {
    display: flex;
    align-items: center;
    justify-content: center;
    .overinover {
      display: flex;
      flex-direction: column;
      justify-content: center;
      gap: 30px;
      color: rgb(255, 217, 0);
      padding: 100px 20px 20px 20px;
      h3 {
        margin-top: -90px;
      }
    }
  }
}
ul {
  padding-left: 110px;
  list-style: none;
  display: flex;
  flex-wrap: wrap;
}
p {
  color: #fff;
  text-shadow: 0 1px 6px rgba(92, 124, 129, 0.9);
}
img {
  width: 230px;
  height: 320px;
  -webkit-box-shadow: 0 1px 6px rgba(57, 73, 76, 0.35);
  box-shadow: 0 1px 6px rgba(57, 73, 76, 0.9);
  padding-right: 2px;
}
.title {
  width: 200px;
}
.titleandvote {
  width: 248px;
  padding: 13px;
  display: flex;
  //   align-content: flex-start;
  justify-content: space-around;
  p {
    font-weight: 900;
  }
  .vote {
    color: #cccccc;
  }
}
</style>
