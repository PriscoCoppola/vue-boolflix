<template>
    <div class="card">
        <!-- Poster -->
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
            <!-- Titolo -->
            <div>
                Titolo:
                <span v-if="info.title === undefined">{{ info.name }}</span>
                <span v-else>{{ info.title }}</span>
            </div>
            <!-- Titolo Originale -->
            <div>
                Titolo Originale:
                <span v-if="info.original_title === undefined">{{
                    info.original_name
                }}</span>
                <span v-else>{{ info.original_title }}</span>
            </div>
            <!-- Lingua -->
            <div>
                Lingua:
                <img
                    v-if="isFlag(info.original_language)"
                    class="language"
                    :src="
                        require(`@/assets/images/${info.original_language}.png`)
                    "
                    :alt="info.original_language"
                />
                <span v-else>{{ info.original_language }}</span>
            </div>
            <!-- Voto -->
            <div>
                Voto:
                <i
                    class="fas fa-star"
                    v-for="(fullStar, i) in Math.round(info.vote_average / 2)"
                    :key="`fullStars${i}`"
                ></i>
                <i
                    class="far fa-star"
                    v-for="(emptyStar, i) in 5 -
                        Math.round(info.vote_average / 2)"
                    :key="`emptyStars${i}`"
                ></i>
            </div>
            <!-- Info -->
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
    data() {
        return {
            flagsImg: ["it", "en"],
        };
    },
    methods: {
        isFlag(lang) {
            return this.flagsImg.includes(lang);
        },
    },
};
</script>

<style lang="scss">
.card {
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
