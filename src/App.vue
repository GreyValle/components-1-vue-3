<script setup>
 import { computed, onMounted, ref } from 'vue';
import BlogPost from './components/BlogPost.vue';
import ButtonCounter from './components/ButtonCounter.vue';
import PaginatePosts from './components/PaginatePosts.vue';
import LoadingSpinners from './components/LoadingSpinners.vue';

/* 
const postsArray = [
  {title: "POST 1", id : 1, body: 'descripción 1', colorText:'primary'},
  {title: "POST 2", id : 2, body: 'descripción 2', colorText:'primary'},
  {title: "POST 3", id : 3, body: 'descripción 3', colorText:'primary'},
  {title: "POST 4", id : 4, colorText:'secondary'}
] */
const postsArray = ref([]);

const loading = ref(true);
const favorito = ref('');

const numsPage = 10;
const inicio = ref(0);
const fin = ref(numsPage);

const setFavoritoMetodo = (title) =>{
  favorito.value = title
}

const next = ()=>{
  inicio.value += numsPage;
  fin.value += numsPage;
}

const prev = ()=>{
  inicio.value -= numsPage;
  fin.value -= numsPage;
}
//propiedad computada
const maxLongitud = computed(()=>{
  return postsArray.value.length;
})

/* onMounted(async() => {
  
  try {
    const respuesta =  await fetch('https://jsonplaceholder.typicode.com/posts');
    postsArray.value = await respuesta.json();
  } catch (error) {
    console.log(error);
  } finally{
    setTimeout(() => {
      loading.value = false;
    }, 2000);
  }

}) */


/* fetch('https://jsonplaceholder.typicode.com/posts')
  .then(resp => resp.json())
  .then(data => {
    postsArray.value = data;
    console.log(data)
    })
    .catch(e => console.log(e))
  .finally(()=> {
    setTimeout(() => {
      loading.value = false;
    }, 2000);
  }); */


const llamarMetodo = async() => {
  
  try {
    const respuesta =  await fetch('https://jsonplaceholder.typicode.com/posts');
    postsArray.value = await respuesta.json();
  } catch (error) {
    console.log(error);
  } finally{
    setTimeout(() => {
      loading.value = false;
    }, 2000);
  }

};
llamarMetodo();

</script>

<template>

  <LoadingSpinners v-if="loading"></LoadingSpinners>
  <div class="container" v-else>
    <h1>APP</h1>
   
    <h2>Mi post favorito: {{favorito}}</h2>
    
  
    <!--<ButtonCounter></ButtonCounter>-->
   
    <PaginatePosts class="mb-2"
      @next = "next"
      @prev = "prev"
      :inicio = "inicio"
      :fin = "fin"
      :maxLongitud = "maxLongitud"
    ></PaginatePosts>

    <BlogPost 
      v-for="post in postsArray.slice(inicio, fin)" 
      :key="post.id" 
      :title="post.title" 
      :id="post.id" 
      :body="post.body" 
      :colorText="post.colorText"
      @setFavoritoProp = "setFavoritoMetodo"
     
    ></BlogPost>
   <!--<BlogPost title="POST 2" :id="2" body="descripción 2" colorText="danger"></BlogPost>-->
   <!--<BlogPost title="POST 3" :id="3" body="descripción 3" colorText="primary"></BlogPost>-->
   <!--<BlogPost title="POST 4" :id="4" colorText="secondary"></BlogPost>-->
    
  </div>

</template>
