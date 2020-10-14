<template>
  <div id="app">
    <About/>
    <div class="content">
      <ShowPosts v-bind:posted="myPost"/>
      <PostPosts @click="updatePosted" />
    </div>
  </div>
</template>

<script>
//<img alt="Vue logo" src="./assets/logo.png">
import About from './components/About.vue'
import ShowPosts from './components/ShowPosts.vue'
import PostPosts from './components/PostPosts.vue'

export default {
  name: 'App',
  components: {
    About,
    ShowPosts,
    PostPosts
  },
  data () {
    return {
      myPost: {}
    }
  },
  methods: {
    updatePosted(newPost) {
      this.myPost = newPost;
    }
  }
}
</script>

<style>

html {
  box-sizing: border-box;
  background-color: #FDFFFC;
}

*,
*::before,
*::after {
  box-sizing: inherit;
}

h1,h2,h3,h4,h5,h6 {
  font-family: 'Oswald', georgia, serif;
}

#app {
  font-family: 'Open Sans', helvetica, arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  padding: 15px;

  max-width: 1000px;
  height: 600px;

  margin: auto;
}


.content {
  
  padding: 15px 0 30px 0;
  height: 100%;
  display: flex;


}
</style>
