<template>
    <div class="cards">
        <ul 
            v-for="film in filmsList"
            :key="film.id"
        
        >
            <li>
                <div class="images">
                    <div v-if="film.backdrop_path === null"><img class="backdrop" src="@/assets/images/no-poster.png" alt=""></div>
                    <div v-else><img class="backdrop" :src="`https://image.tmdb.org/t/p/w342${film.poster_path}`" alt=""></div>
                    <div class="onhover">
                        <div v-if="film.title === undefined">Titolo: {{ film.name }}</div>
                        <div v-else>Titolo: {{ film.title }}</div>
                        <div v-if="film.original_title === undefined">Titolo: {{ film.original_name }}</div>
                        <div v-else>Titolo: {{ film.original_title }}</div>
                        <div v-if="film.original_language === 'it'">Lingua: <img class="language" src="@/assets/images/it.png" alt="it" /></div>
                        <div v-else-if="film.original_language === 'en'">Lingua: <img class="language" src="@/assets/images/en.png" alt="en" /></div>
                        <div v-else>Lingua: {{ film.original_language }}</div>
                        <div>Voto:
                            <span
                                v-for="(fullStar, x) in Math.round(film.vote_average / 2)"
                                :key="x + 1000"
                            ><i class="fas fa-star"></i></span>
                            <span
                                v-for="(emptyStar, i) in 5 - Math.round(film.vote_average / 2)"
                                :key="i"
                            ><i class="far fa-star"></i></span>
                        </div>
                        <div>Info: {{ film.overview }}</div>
                    </div>
                </div>
            </li>
        </ul>
    </div>
</template>

<script>

export default {
    name: "Content",
    props: ['filmsList'],
};
</script>

<style lang="scss" scoped>
.cards {
    display: flex;
    flex-wrap: wrap;
    margin: 0 40px;

    ul {
        list-style: none;
        margin: 20px 10px;
        
        .images {
            position: relative;
            height: 500px;

            &:hover .onhover {
                display: flex;
            }

            .backdrop {
                width: 342px;
                height: 500px;
            }
            
            .onhover {
                display: none;
                flex-direction: column;
                justify-content: center;
                position: absolute;
                top: 0;
                left: 0;
                right: 0;
                bottom: 0;
                padding: 20px; 
                background-color: rgba(0, 0, 0, .8);
                color: #fff;
                overflow: auto;

                div {
                    padding-bottom: 10px;

                    i {
                        color: yellow;
                    }
                }

                .language {
                    width: 20px;
                    height: 10px;
                }
            }
        }  
    }
}



</style>
