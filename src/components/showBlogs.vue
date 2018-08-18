<template>
    <div v-theme:column="''" id="show-blogs">
        <h3>Semua Artikel Blog</h3>
        <input type="text" v-model="search" placeholder="Cari ..." />
        <div v-for="blog in filteredBlogs" class="single-blog">
            <router-link id="myblogtitle" v-bind:to="'/blog/' + blog.id"><h2>{{ blog.title | to-uppercase }}</h2></router-link>
            <article>{{ blog.content | snippet }}</article>
        </div>
    </div>
</template>

<script>
import searchMixin from '../mixins/searchMixin.js';

export default {
  data() {
    return {
        blogs: [],
        search: ''
    }
  },
  methods: {
  },
  created() {
      this.$http.get('https://simple-vue-blog-b4ddf.firebaseio.com/posts.json').then(function(data){
          return data.json();
      }).then(function(data){
        var blogsArray= [];
        for (let key in data) {
            data[key].id = key
            blogsArray.push(data[key]);
        }
        this.blogs = blogsArray;
      })
  },
  computed: {
      
  },
  filters: {
      toUppercase(value){
          return value.toUpperCase();
      }
  },
  directives: {
      'rainbow':{
        bind(el,binding,vnode){
          el.style.color = "#" + Math.random().toString(16).slice(2,8);
            }
      }
  },
  mixins: [searchMixin]
}
</script>

<style>

#show-blogs {
    max-width: 800px;
    margin: 0 auto;
    font-family: 'M PLUS Rounded 1c', sans-serif;
}

#myblogtitle {
    text-decoration: none;
    color: #717171;
}

#myblogtitle:hover {
    color: coral;
}

input {
    width: 100%;
    border: .5px solid grey;
    /* border-radius: 20px; */
    height: 30px;
    font-size: 20px;
}


.single-blog{
    padding: 20px;
    margin: 20px 0;
    box-sizing: border-box;
    background: #eee;
}
</style>