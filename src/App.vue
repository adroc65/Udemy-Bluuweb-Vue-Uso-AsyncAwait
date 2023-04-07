<script setup>
  
  import BlogPost from './components/BlogPost.vue';
  import PaginatePost from './components/PaginatePost.vue';
  import LoadingSpinner from './components/LoadingSpinner.vue';
  //import ButtonCounter from './components/ButtonCounter.vue';

  import { ref, computed, onMounted } from 'vue';

  const posts1 = ref([
    {
      id: 1,
      title:"La Flaca", 
      bgColor: "primary",
      textColor: "light", 
      body: "En la vida conocí, Mujer igual a la flaca, Coral negro de la Habana, Tremendísima mulata",
    },
    {
      id: 2,
      title: "El Lado Oscuro",  
      bgColor:"secondary",
      textColor:"light",
      body:"Puede que hayas, Nacido en la cara buena del mundo, yo nací en la cara mala, llevo la marca del lado oscuro",
    },
    {
      id: 3,
      title: "Angel", 
    },
  ]);

  const favorito = ref('');

  const cambiarFavorito = (title, id) => {
    favorito.value = `${id} - ${title}`
  }

  // Paginador
  const postXpagina = 10;
  const inicio = ref(0);
  const fin = ref(postXpagina);
  const next = () => {
    inicio.value += postXpagina
    fin.value += postXpagina
  }
  const prev = () =>{
    inicio.value -= postXpagina
    fin.value -= postXpagina
  }
  const maxLength = computed(() => posts.value.length)

  // Loading ...
  const loading = ref(true);
  
  //  Leer Posts, es externo, mejor usar ASYNC y AWAIT
  const posts = ref([]);

  onMounted(() => {
    fetchData();
  });

  /*fetch("https://jsonplaceholder.typicode.com/posts")
    .then((res) => res.json())
    .then((data) => posts.value = data)
    .catch((e) => console.log(e))
    .finally(() => {
      setTimeout(() =>{ loading.value = false }, 1000)
    })*/

  const fetchData = async () => {
    try {
      const res = await fetch("https://jsonplaceholder.typicode.com/posts");
      posts.value = await res.json();
    } catch (error) {
      console.log(error)
    } finally {
      setTimeout(() =>{ loading.value = false }, 1000)
    }
  }

</script>

<template>
  <LoadingSpinner v-if="loading" />
  <div v-else class="container">
    <h1>APP</h1>
    <h2> Mi Post favorito: </h2>
    <p class="border border-success p-2 text-center">{{ favorito }}</p>

    <PaginatePost 
      :inicio="inicio"
      :fin="fin"
      :maxLength="maxLength"
      @next="next"
      @prev="prev"
    />

    <BlogPost 
      v-for="post in posts.slice(inicio, fin)"
        :key="post.id"
        :title="post.title"
        :id="post.id"
        :body="post.body"
        :bgColor="post.bgColor"
        :textColor="post.textColor"
        @cambiarFavorito="cambiarFavorito"
    ></BlogPost>
  </div>
  
</template>

<style scoped>

</style>
