<template>
  <div id="add-blog">

    <h2>Add new blog post</h2>

    <form v-if="!submitted">
        <label>Blog title:</label>
        <input type="text" v-model.lazy="blog.title">
        <label>Blog content:</label>
        <textarea rows="10" v-model.lazy="blog.content"></textarea>

        <div id="checkboxes">
            <label for="">Frameworks</label>
            <input type="checkbox" value="Frameworks" v-model="blog.categories">
            <label for="">Node</label>
            <input type="checkbox" value="Node Js" v-model="blog.categories">
            <label for="">Javascript</label>
            <input type="checkbox" value="Javascript" v-model="blog.categories">
        </div>

        <label>Author: </label>

        <select v-model="blog.author">
            <option v-for="(author, index) in authors" v-bind:key='index'> {{ author }} </option>
        </select>

        <br>

        <button v-on:click.prevent="post()">Add blog</button>

    </form>

    <div v-if="submitted">
        <h3>Thanks for adding a post!</h3>
    </div>

    <div>
        <h3 v-if="verif">Please fill the post information</h3>
    </div>

    <div class="preview">
        <h3>Preview post</h3>
        <p>Blog title: {{ blog.title }} </p>
        <p>Blog content: </p>
        <p> {{ blog.content }} </p>
        <p>Blog Categories</p>
        <ul>
            <li v-for='(category, index) in blog.categories' v-bind:key="index"> {{ category }} </li>
        </ul>
        <p>Author: {{ blog.author }}</p>
    </div>

  </div>
</template>

<script>

export default {
    data() {
        return {
            blog: {
                title: '',
                content: '',
                categories: [],
                author: ''
            },
            authors: ['Patrick Passarella', 'Paris Meave', 'Vue Ninja'],
            submitted: false,
            verif: false
        }
    },
    methods: {
        post () {

            if (this.blog.title === '' || this.blog.content === '') {
                this.verif = true;
            } else {
                this.verif = false;
                this.$http.post('https://jsonplaceholder.typicode.com/posts', {
                    title: this.blog.title,
                    body: this.blog.content,
                    userId: 1
                }).then((data) => {
                    console.log(data);
                    this.submitted = true;
                })
            }

            
        }
    }
}
    
</script>

<style scoped>

#add-blog * {
    box-sizing: border-box;
}

#add-blog {
    margin: 20px auto;
    max-width: 500px;
}

#add-blog label {
    display: block;
    margin: 20px 0 10px;
}

#add-blog input {
    display: block;
    width: 100%;
    padding: 8px;
}

#add-blog textarea {
    width: 100%;
}

#add-blog .preview {
    padding: 10px 20px;
    border: 1px solid #ccc;
    margin: 30px 0;
}

h3 {
    margin-top: 10px;
}

#checkboxes{
    display: flex;
    align-items: baseline;
}

#checkboxes label {
    display: inline-block;
}

#add-blog button {
    margin-top: 20px;
    font-size: 16px;
    font-weight: 100;
    padding: 8px;
    background: none;
}

</style>

