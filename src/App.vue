<script>
import axios from 'axios';

export default {
  data() {
    return { 
      apikey: '3a4db1cb907349cc970d7a7e93db75c6',
      searchText: '',
      movies:[],
      series:[]
      
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
        console.log('MOVIES', resp.data);

        this.movies = resp.data.results;
      });
      axios
      .get('https://api.themoviedb.org/3/search/tv',{
        params:{
          api_key: this.apikey,
          query: this.searchText,

        }
      })
      .then((resp) => {
        console.log('SERIES',resp.data);

        this.series = resp.data.results;
      });
        
        
      }
    }  
  }

</script>

<template>
  <div>
    <div class="container py-5">
      <div class="d-flex justify-content-between">
        <form @submit.prevent="search">
          <input v-model="searchText" type="text" placeholder="Cerca film o serie TV..">
          <button type="submit">
            Cerca
          </button>
        </form>
        <h1>BOOLFLIX</h1>
      </div>
    </div>
    <div>
      <h2 class="text-center py-5">
        Movies
      </h2>
      <hr>
      <ol>
        <li v-for="(movie, i) in movies" :key="i">
          <ul>
            <li>
              Titolo: {{ movie.title }}
            </li>
            <li>
              Titolo originale: {{ movie.original_title }}
            </li>
            <li>
              <template v-if="movie.original_language == 'en'">
                Lingua: <img src="/img/flags/uk.gif" alt="">
              </template>
              <template v-else-if="movie.original_language == 'it'">
                Lingua: <img src="/img/flags/it.gif" alt="">
              </template>
              <template v-else-if="movie.original_language == 'jp'">
                Lingua: <img src="/img/flags/ja.gif" alt="">
              </template>
              <template v-else-if="movie.original_language == 'us'">
                Lingua: <img src="/img/flags/us.gif" alt="">
              </template>
            </li>
            <li>
              Voto:{{ movie.vote_average }}
            </li>
          </ul>
        </li>
      </ol>
    </div>
    <div>
      <h2 class="text-center py-5">
        Series
      </h2>
      <ol>
        <li v-for="(serie, i) in series" :key="i">
          <ul>
            <li>
              Titolo: {{ serie.name }}
            </li>
            <li>
              Titolo originale: {{ serie.original_name }}
            </li>
            <li>
              <template v-if="serie.original_language == 'en'">
                Lingua: <img src="/img/flags/uk.gif" alt="">
              </template>
              <template v-else-if="serie.original_language == 'it'">
                Lingua: <img src="/img/flags/it.gif" alt="">
              </template>
              <template v-else-if="serie.original_language == 'jp'">
                Lingua: <img src="/img/flags/ja.gif" alt="">
              </template>
              <template v-else-if="serie.original_language == 'us'">
                Lingua: <img src="/img/flags/us.gif" alt="">
              </template>
            </li>
            <li>
              Voto:{{ serie.vote_average }}
            </li>
          </ul>
          <hr>
        </li>
      </ol>
    </div>
  </div>
</template>

<style lang="scss">


// Import all of Bootstrap's CSS
@import "bootstrap/scss/bootstrap";
img{
  max-width: 30px;
}
h1{
  color: red;
}
h2{
  color: red;
}
</style>
