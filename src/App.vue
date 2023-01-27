<script>
import axios from 'axios';
import { api } from './data';
import { store } from './data/store';
import SearchBar from './components/SearchBar.vue';
import ProductionCard from './components/productions/ProductionCard.vue'
export default {
  name: 'Boolflix',
  components: {SearchBar, ProductionCard},
  data(){
    return {
      store,
      titleFilter: ''
    }
  },
  computed: {
    axiosConfig(){
      const { key, language } = api;
      return {
        params: {
          api_key: key,
          language: language,
          query: this.titleFilter
        }
      }
    }
  },
  methods: {
    onTitleFilter(term){
      this.titleFilter = term
    },
    searchProductions() {
      if(!this.titleFilter){
        this.movies = [];
        this.series = [];
        return;
      }

      this.fetchApi('search/movie', 'movies');
      this.fetchApi('search/tv', 'series');
    },
    fetchApi(endpoint, collection){
      axios.get(`${api.baseUri}/${endpoint}`, this.axiosConfig)
      .then(res => {
        store[collection] = res.data.results;
      }).catch(err => {console.error(err)});
    }

  }
};
</script>

<template>
  <header>
    <search-bar placeholder="Cerca un film" @term-change="onTitleFilter" @form-submit="searchProductions"></search-bar>

  </header>

  <main>
    <section>
      <h2>Movies</h2>
      <production-card v-for="movie in store.movies" :key="movie.id" :item="movie"></production-card>  
    </section>
    <section>
      <h2>Series</h2>
      <production-card v-for="serie in store.series" :key="serie.id" :item="series"></production-card> 
    </section>
  </main>
 
</template>

<style>
 
</style>