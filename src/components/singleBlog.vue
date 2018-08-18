<template>
    <div id="single-blog">
        <h1>{{ blog.title }}</h1>
        <hr>
        <p>Oleh: {{ blog.author }}</p>
        <br>
        <article>{{ blog.content }}</article>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                id: this.$route.params.id,
                blog:{}
            }
        },
        created(){
            this.$http.get('https://simple-vue-blog-b4ddf.firebaseio.com/posts/'+this.id + '.json').then(function(data){
                return data.json();
            }).then(function(data){
                this.blog = data;
            });
        }
    }
</script>

<style>
#single-blog{
    max-width: 960px;
    margin: 0 auto;
}

h1 {
    color: coral;
    font-size: 50px;
}

p {
    color: salmon;
}
</style>