<template>
  
    <div id="show-blogs">
        <h2>All blog articles</h2>
        <div v-for="(post, index) in posts" v-bind:key="index" class="single-post">
            <h2 v-rainbow> {{ post.title }} </h2>
            <p> {{ post.body }} </p>
        </div>
    </div>

</template>

<script>
    
    export default {
        data () {
            return {
                posts: []
            }
        },
        created () {
            this.$http.get("https://jsonplaceholder.typicode.com/posts").then( (data) => {
                console.log(data);
                this.posts = data.body.slice(0, 10);
            })
        }
    }

</script>

<style scoped>

#show-blogs {
    max-width: 800px;
    margin: 0 auto;
}

#show-blogs .single-post {
    padding: 20px;
    margin: 20px 0;
    box-sizing: border-box;
    background: #eee;
    color: #222;
}

</style>
