<script>
export default {
    name: 'ProductionCard',

    props: {
        item: Object
    },
    computed: {
        title() {
            return this.item.title || this.item.name;
        },
        originalTitle() {
            return this.item.original_title || this.item.original_name;
        },
        hasFlag() {
            const flags = ['it', 'en'];
            return flags.includes(this.item.original_language);
        },
        flagSrc() {
            const url = new URL(`../../assets/img/${this.item.original_language}.png`, import.meta.url);
            return url.href;
        },

    },
    methods: {
        getStars(average) {
            return Math.ceil(average / 2);
        },
        getVoidStars(average) {
            return 5 - Math.ceil(average / 2);
        },
    }

};
</script>

<template>
    <ul>
        <li>{{ title }}</li>
        <li>{{ originalTitle }}</li>
        <img :src="`https://image.tmdb.org/t/p/w342/${item.poster_path}`">
        <li>
            <img v-if="hasFlag" :src="flagSrc" :alt="item.original_language">

            <div v-else>{{ item.original_language }}</div>
            <div>
                <font-awesome-icon v-for="star in getStars(item.vote_average)" icon="fa-solid fa-star" />
                <font-awesome-icon v-for="star in getVoidStars(item.vote_average)" icon="fa-regular fa-star" />
            </div>
        </li>
    </ul>
</template>

<style>

</style>
