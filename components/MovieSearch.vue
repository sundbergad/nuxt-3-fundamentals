<script  setup>
const query = ref("");
const movies = ref([]);
let RequestInit = query.value;
async function search(){
    // use an utility function from nuxt, $fetch
    // await $fetch('https://www.omdbapi.com/?i=tt3896198&apikey=88188528&t=' , query.value)
    // .then (response =>{
    //     console.log(response);
    //     if(response.OK) then
    //         movies.value = response;
    //         console.log(movies.value);            
    // })
    // .catch(error => {
    //     console.log(error);
    // })

    // };
    const Search = await $fetch('http://www.omdbapi.com/?i=tt3896198&apikey=88188528&t=' , query.value);
    if(Search.Response == "OK"){
        movies.value = Search;
        console.log(Search);
    }else{
        movies.value[0] = Search;
        console.log(Search);
    }
    
    console.log(Search.Title);
}
</script>

<template>
  <div>
    <form @submit.prevent="search">
        <input type="text" v-model="query">
        <button>Search</button>
    </form>
    <!-- {{ movies }} -->
    <p v-for="m in movies" :key="movies.imdbID"><img :src="m.Poster" /></p>
        <ul  style="display: flex; flex-wrap: wrap; gap: 10px; list-style: none">
            <li v-for="movie in movies" :key="movie.imdbID">{{ movie.Title }}
            <NuxtLink :to="{ name: 'movies-id', params: { id: movie.imdbID } }">{{ movie.imdbID }}
                <!-- <img :src="movie.Poster" :alt="movie.title" width="100" /> -->
            </NuxtLink>
            </li>
        </ul>
  </div>
</template>

<style scoped></style>
