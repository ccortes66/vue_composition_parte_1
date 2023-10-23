<script setup>
 import {computed, onMounted, ref} from 'vue'

 import BlogPost from './components/BlogPost.vue';
 import ButtonPagination from './components/ButtonPagination.vue';
 
 const numItems = 10
 const inicio = ref(0)
 const fin = ref(numItems)

 const loading = ref(true)
 const favorito = ref(" ")
 
 const next = () => { 
     inicio.value += numItems
     fin.value += numItems 
  }
 
 const previous = () =>{
    inicio.value -= numItems
    fin.value -= numItems
 } 

 const favoritePost = (title) => favorito.value = title
 
 onMounted(async () =>{
   try 
   {
     const result =  await fetch('https://jsonplaceholder.typicode.com/posts') 
     posts.value = await result.json()
   } 
   catch (error) { console.error(error)}
   finally { 
      setInterval(() =>{
         loading.value = false
      },2000)
      
   }
 })
 const posts = ref([])
 /*
 fetch('https://jsonplaceholder.typicode.com/posts')
 .then(res => res.json())
 .then(data => posts.value = data )
 .catch(console.error)
 .finally( ()=>{
    setTimeout(() => {
      loading.value = false
    },2000)
 })
 */

 const maxLength = computed(() => posts.value.length)
</script>

<template>
  
  <section v-if="loading" class="d-flex flex-column  align-items-center">
      <div class="spinner-border mt-5" role="status">
      </div>
       <p >Loading...</p>
  </section>
  
  
  <section v-else class="container">
    <h1>APP</h1>
    <h2>Post favorito: {{ favorito }}</h2>
  
    <ButtonPagination 
            class="mb-2" 
            @prev="previous"
            @next="next"

            :inicio="inicio"
            :fin="fin"
            :largo="maxLength"
    />
    <BlogPost
       v-for="post in posts.slice(inicio,fin)"
       :key="post.id"
       
       :id="post.id"
       :title="post.title"
       :body="post.body"
       :class="'mb-2'"
       @favoritePostName="favoritePost"
       >

    </BlogPost>
  </section>
</template>

