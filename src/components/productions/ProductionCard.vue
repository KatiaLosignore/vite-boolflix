<script>
import { pics } from '../../data';
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
        posterPath() {
            if (!this.item.poster_path) return pics.placeholder;
            return pics.baseUrl + this.item.poster_path;
        },
        longText() {
            return this.item.overview.length  > 265 ? this.item.overview.substring(0, 265) + '...' : this.item.overview;
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
    <section id="cards">
        <div class="image">

            <img :src="posterPath" :alt="title" class="img-fluid mb-3 card-image">
        </div>
        <div class="description">
            <p class="text-white"><strong>Titolo: </strong>{{ title }}</p>
            <p class="text-white"><strong>Titolo originale: </strong>{{ originalTitle }}</p>

            <div>
                <img class="size-flag mb-2" v-if="hasFlag" :src="flagSrc" :alt="item.original_language">
                <p class="text-white fw-bold" v-else>{{ item.original_language }}</p>

                <span class="text-white fw-bold">Voto: </span>
                <font-awesome-icon v-for="star in getStars(item.vote_average)" icon="fa-solid fa-star" class="star" />
                <font-awesome-icon v-for="star in getVoidStars(item.vote_average)" icon="fa-regular fa-star"
                    class="star" />

                <p class="text-white"><strong>Overwiew: </strong> {{ longText }}</p>
            </div>

        </div>

    </section>

</template>

<style lang="scss" scoped>
@use '../../assets/scss/partials/variables' as *;

#cards {
    width: 300px;
    margin: 0 6px;

    .card-image {
        width: 300px;
        height: 400px;
        background-color: $white;
    }
}

.description {
    background-color: $black;
    width: 100%;
    height: 400px;
    padding: 8px;
    display: none;

    .size-flag {
        width: 60px;
    }

    .star {
        color: $yellow;
    }

}


#cards:hover .description {
    display: block;
    width: 100%;
    cursor: pointer;
    position: relative;
    z-index: 1;
}

#cards:hover .image {
    display: none;
}
</style>
