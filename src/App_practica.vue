<script setup>
 import BlogPost from './components/BlogPost.vue' 
 import {ref} from 'vue'

 const posts = ref([
  {title:"Post 1", content:"content 1", id:1},
  {title:"Post 2", id:2},
  {title:"Post 3", content:"content 3", id:3},
  {title:"Post 4", content:"content 1", id:4}
 ])

 const favorite = ref("")
 const favoritePost = (title) =>{
  favorite.value = title
 }
</script>

<template>
  <section class="container">
    <h1>app</h1>
    <h2>Favorite post {{ favorite }}</h2>

    <BlogPost
           v-for="post in posts"
           :key="post.id" 

           :title="post.title" 
           :content="post.content" 
           :id="post.id"
           @favoritePostName="favoritePost"
           >
    </BlogPost>
    
  </section>
</template>

<style>

</style>