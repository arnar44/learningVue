<template>
  <div class="hello">
    <h1>Vue exercise</h1>
    <p>
      This is a simple Vue app that interacts with a test API. The API is https://jsonplaceholder.typicode.com/ 
      which a simple API designed to help developers test API calls. The purpose of this app is to learn the Vue syntax. 
    </p>
    <p>
      Note: Since this is a test API, users are not allowed to actually post to it. When a user posts the response is revived to
      check for errors, if successful the post is added to the posts manually, but they will disappear when posts are fetched.
    </p>
  </div>
</template>

<script>
export default {
  name: 'About',
  props: {
    msg: String
  }
}
</script>

<style scoped>
  h1 {
    text-align: center;
  }
</style>
