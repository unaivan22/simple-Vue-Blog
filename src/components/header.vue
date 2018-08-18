<template>
    <!-- <div class="container"> -->
    <div class="col m6 text-center">
    <nav>
        <ul>
            <li><router-link to="/" exact>Blog</router-link></li>
            <li><router-link to="/add" exact>Tambah Baru</router-link></li>
        </ul>
    </nav>
    </div>
<!-- </div> -->
</template>

<script>

</script>

<style scoped>
ul{
    list-style-type: none;
    text-align: center;
    margin: 0;
}
li{
    display: inline-block;
    margin: 0 10px;
}
a{
    color: #fff;
    text-decoration: none;
    padding: 6px 8px;
    border-radius: 10px;
}

nav {
    background: #17181e;
    padding: 14px 0;
    margin-bottom: 40px;
}
.router-link-active{
    background: #eee;
    color: #444;
}
</style>


export default {

}