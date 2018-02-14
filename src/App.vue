<template>
  <div id="app">
    
      <show-blogs></show-blogs>

  </div>
</template>

<script>

import addBlog from './components/addBlog.vue'
import showBlogs from './components/showBlogs'

export default {
  components: {
    'add-blog': addBlog,
    'show-blogs': showBlogs
  },
  data () {
    return {
      
    }
  }
}
</script>

<style>

  body {
    font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
    font-weight: 100;
    margin: 0;
  }

</style>
