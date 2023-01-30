<script>
import axios from 'axios';
import { api } from '../data';
import { store } from '../data/store';
import SearchBar from './searchbar/SearchBar.vue';
export default {
    name: 'AppHeader',
    components: { SearchBar },
    data() {
        return {
            store,
            titleFilter: '',
        }
    },
    computed: {
        axiosConfig() {
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
        onTitleFilter(term) {
            this.titleFilter = term
        },
        searchProductions() {
            if (!this.titleFilter) {
                store.movies = [];
                store.series = [];
                return;
            }

            this.fetchApi('search/movie', 'movies');
            this.fetchApi('search/tv', 'series');
        },
        fetchApi(endpoint, collection) {
            axios.get(`${api.baseUri}/${endpoint}`, this.axiosConfig)
            .then(res => {
            store[collection] = res.data.results;
            }).catch(err => { console.error(err) });
        }

    }
};
</script>

<template>

    <header>
        <search-bar placeholder="Cerca un film" @term-change="onTitleFilter"
        @form-submit="searchProductions"></search-bar>
    </header>
    
</template>