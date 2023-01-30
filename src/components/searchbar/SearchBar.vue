<script>
export default {
    name: 'SearchBar',
    data() {
        return { term: '' }
    },
    props: {
        placeholder: String,
        buttonLabel: String,
    },
    emits: ['term-change', 'form-submit']
};
</script>

<template>
    
    <nav class="navbar navbar-expand-lg bg-body-tertiary">
        <div class="container">
            <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarTogglerDemo03"
                aria-controls="navbarTogglerDemo03" aria-expanded="false" aria-label="Toggle navigation">
                <span class="navbar-toggler-icon"></span>
            </button>
            <a class="navbar-brand fw-bold size" href="#">BOOLFLIX</a>

            <form @submit.prevent="$emit('form-submit')">
                <input type="text" v-model.trim='term' @keyup="$emit('term-change', term)"
                    :placeholder="placeholder || 'Cerca'">
                <button type="submit" class="text-white fw-normal size-button">{{ buttonLabel || 'Cerca' }}</button>
            </form>
        </div>
    </nav>
    

</template>

<style lang="scss" scoped>
@use '../../assets/scss/partials/variables' as *;

nav {
    height: 80px;

    a.size {
    color: $red;
    font-size: 35px;
    }   
}

.size-button {
    padding: 3px 5px;
    background-color: $red ;
}
.bg-body-tertiary {
    background-color: $black !important;
}

</style>
