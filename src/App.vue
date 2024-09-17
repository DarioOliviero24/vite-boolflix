<script>
import axios from 'axios';

export default {
  data() {
    return { 
      apikey: '3a4db1cb907349cc970d7a7e93db75c6',
      searchText: '',
      movies:[]
      
    }
  },
  methods: {
    search() {
      console.log(this.searchText);  

      axios
      .get('https://api.themoviedb.org/3/search/movie',{
        params:{
          api_key: this.apikey,
          query: this.searchText,

        }
      })
      .then((resp) => {
        console.log(resp.data);

        this.movies = resp.data.results;
      });
        
        
      }
    }  
  }

</script>

<template>
  <div class="">
    <div class="container py-5">
      <div class="d-flex justify-content-between">
        <form @submit.prevent="search">
          <input v-model="searchText" type="text" placeholder="Cerca film o serie TV..">
          <button type="submit">
            Cerca
          </button>
        </form>

      </div>
    </div>
    <div>
      <ol>
        <li v-for="(movie, i) in movies" :key="i">
          <ul>
            <li>
              {{ movie.poster_path }}
            </li>
            <li>
              Titolo: {{ movie.title }}
            </li>
            <li>
              Titolo originale: {{ movie.original_title }}
            </li>
            <li>
              Lingua:{{ movie.original_language }}
            </li>
            <li>
              Voto:{{ movie.vote_average }}
            </li>
          </ul>
          <hr>
        </li>
      </ol>
    </div>
  </div>
</template>

<style lang="scss">
.BG{
  background-color: black;
  color: white;
  height: 100vh;
}

// Import all of Bootstrap's CSS
@import "bootstrap/scss/bootstrap";

</style>
