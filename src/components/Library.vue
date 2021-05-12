<template>
    <div class="images">
        <div v-if="info.backdrop_path === null">
            <img class="backdrop" src="@/assets/images/no-poster.png" alt="" />
        </div>
        <div v-else>
            <img
                class="backdrop"
                :src="`https://image.tmdb.org/t/p/w342${info.poster_path}`"
                alt=""
            />
        </div>
        <div class="onhover">
            <div v-if="info.title === undefined">Titolo: {{ info.name }}</div>
            <div v-else>Titolo: {{ info.title }}</div>
            <div v-if="info.original_title === undefined">
                Titolo: {{ info.original_name }}
            </div>
            <div v-else>Titolo: {{ info.original_title }}</div>
            <div v-if="info.original_language === 'it'">
                Lingua:
                <img class="language" src="@/assets/images/it.png" alt="it" />
            </div>
            <div v-else-if="info.original_language === 'en'">
                Lingua:
                <img class="language" src="@/assets/images/en.png" alt="en" />
            </div>
            <div v-else>Lingua: {{ info.original_language }}</div>
            <div>
                Voto:
                <span
                    v-for="(fullStar, x) in Math.round(info.vote_average / 2)"
                    :key="x + 1000"
                    ><i class="fas fa-star"></i
                ></span>
                <span
                    v-for="(emptyStar, i) in 5 -
                        Math.round(info.vote_average / 2)"
                    :key="i"
                    ><i class="far fa-star"></i
                ></span>
            </div>
            <div>Info: {{ info.overview }}</div>
        </div>
    </div>
</template>

<script>
export default {
    name: "Library",
    props: {
        info: Object,
    },
};
</script>

<style lang="scss">
.images {
    padding: 0 10px;
    position: relative;
    height: 505px;

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
        background-color: rgba(0, 0, 0, 0.8);
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
</style>
