<template>
    <div class="cards">
        <ul 
            v-for="(film, i) in filmsList"
            :key="i"
        
        >
            <li><img :src="`https://image.tmdb.org/t/p/w300${film.backdrop_path}`" alt=""></li>
            <li v-if="film.title === undefined">Titolo: {{ film.name }}</li>
            <li v-else>Titolo: {{ film.title }}</li>
            <li v-if="film.original_title === undefined">Titolo: {{ film.original_name }}</li>
            <li v-else>Titolo: {{ film.original_title }}</li>
            <li v-if="film.original_language === 'it'">Lingua: <img class=".language" src="@/assets/images/it.png" alt="it" /></li>
            <li v-else-if="film.original_language === 'en'">Lingua: <img class="language" src="@/assets/images/en.png" alt="en" /></li>
            <li v-else>Lingua: {{ film.original_language }}</li>
            <li>Voto: {{ film.vote_average }}</li>
        </ul>
    </div>
</template>

<script>

export default {
    name: "Content",
    props: ['filmsList'],
    data() {
        return {
            
        };
    },
    methods: {
        
    },
};
</script>

<style lang="scss" scoped>
.language {
    width: 20px;
    height: 10px;
}
</style>
