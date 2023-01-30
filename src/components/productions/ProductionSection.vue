<script>
import { store } from '../../data/store';
import ProductionCard from './ProductionCard.vue';
export default {
    name: 'ProductionSection',
    components: { ProductionCard },
    props: {
        title: String,
        collection: String
    },
    data() {
        return { store }
    }
};
</script>

<template>
    <div class="container">
        <section :id="collection">
            <h2 class="text-white mt-3">{{ title }}</h2>
            <div class="d-flex flex-wrap">
              <production-card v-for="production in store[collection]" :key="production.id" :item="production"></production-card>
            </div>
        </section>
    </div>
</template>


