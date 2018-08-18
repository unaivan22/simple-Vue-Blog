<template>
  <div id="add-blog">
    <h2>Tambah Tulisan Baru</h2>
    <p id="nb">#Mohon direfresh kembali bila tampilan berantakan</p>
    <hr>
    <form v-if="!submitted">
        <label>Judul Blog:</label>
        <input type="text" v-model.lazy="blog.title" required />
        <label>Konten Blog</label>
        <textarea v-model.lazy="blog.content"></textarea>
        <div id="checkboxes">
            <label>Teknologi</label>
            <input class="filled-in" type="checkbox" value="teknologi" v-model="blog.categories">
            <label>Hiburan</label>
            <input type="checkbox" value="hiburan" v-model="blog.categories">
            <label>Sport</label>
            <input type="checkbox" value="sport" v-model="blog.categories">
            <label>Style</label>
            <input type="checkbox" value="style" v-model="blog.categories">
            <label>Humor</label>
            <input type="checkbox" value="humor" v-model="blog.categories">
        </div>
        <label>Penulis:</label>
        <select v-model="blog.author">
            <option v-for="author in authors">{{ author }}</option>
        </select>    
        <br>
        <br>
        <button class="waves-effect waves-light btn" v-on:click.prevent="post">Posting Tulisan</button>
    </form>
    <div v-if="submitted">
        <h3>Terima Kasih sudah menambah tulisan baru</h3>
    </div>
    <div id="preview">
        <h3>Preview Blog</h3>
        <p>Judul Blog: {{blog.title}}</p>
        <p>Konten Blog:</p>
        <p>{{blog.content}}</p>
        <p>Kategori:</p>
        <ul>
            <li v-for="category in blog.categories">{{ category }}</li> 
        </ul>
        <p>Penulis: {{ blog.author }}</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
        blog: {
            title:"",
            content:"",
            categories: [],
            author: ""
        },
        authors:['Eka Ramadayanti', 'unaivan'],
        submitted: false,
    }
  },
  methods: {
      post: function(){
          this.$http.post('https://simple-vue-blog-b4ddf.firebaseio.com/posts.json',this.blog).then(function(data){
              console.log(data);
              this.submitted = true;
          });
      }
  }
}
</script>

<style>
#add-blog *{
    box-sizing: border-box;
}

#add-blog{
    font-family: 'M PLUS Rounded 1c', sans-serif;
    margin: 20px auto;
    max-width: 500px;
}

label {
    display: block;
    margin: 20px 0 10px;
}

input[type="text"],textarea{
    display: block;
    width: 100%;
    padding: 8px;
}

#preview {
    padding: 10px 20px;
    border: 1px dotted #ccc;
    margin: 30px 0;
}

#nb {
    color: salmon;
}

h3{
    margin-top: 10px;
}

#checkboxes {
    display: inline;
}

#checkboxes input{
    display: inline-block;
    margin-right: 10px;
}

select {
    width: 50%;
    height: 30px;
}

button {
    font-family: 'M PLUS Rounded 1c', sans-serif;
    border-radius: 30px;
    border: none;
    outline: 0;
    display: inline-block;
    padding: 10px 25px;
    color: black;
    background-color:#E6BC0F;
    text-align: center;
    cursor: pointer;
}

#checkboxes label{
    display: inline-block;
}

</style>