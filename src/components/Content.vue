<template>
    <main>
        <div class="screenOne" v-show="screenOne">
            <!-- Search List -->
            <div
                class="searchList"
                v-if="filmsList.length !== 0 || seriesList.length !== 0"
            >
                <!-- Movies -->
                <h1 v-show="filmsList.length !== 0">Movies</h1>
                <div class="cards">
                    <Library
                        v-for="film in filmsList"
                        :key="film.id"
                        :info="film"
                        @infoBig="showInfo"
                    />
                </div>
                <!-- Series -->
                <h1 v-show="seriesList.length !== 0">Series</h1>
                <div class="cards">
                    <Library
                        v-for="series in seriesList"
                        :key="series.id"
                        :info="series"
                        @infoBig="showInfo"
                    />
                </div>
            </div>
            <!-- Homepage -->
            <div class="homepage" v-else>
                <!-- Popular -->
                <h1>Popular</h1>
                <div class="cards">
                    <Library
                        v-for="popular in popularList"
                        :key="popular.id"
                        :info="popular"
                        @infoBig="showInfo"
                    />
                </div>
                <!-- Top Rated -->
                <h1>Top Rated</h1>
                <div class="cards">
                    <Library
                        v-for="topRated in topRatedList"
                        :key="topRated.id"
                        :info="topRated"
                        @infoBig="showInfo"
                    />
                </div>
            </div>
        </div>
        <div class="screenTwo container" v-show="screenTwo">
            <!-- Poster -->
            <div v-if="infoObj.backdrop_path === null">
                <img
                    class="backdrop"
                    src="https://slack-imgs.com/?c=1&o1=ro&url=https%3A%2F%2Fwww.altavod.com%2Fassets%2Fimages%2Fposter-placeholder.png"
                    alt=""
                />
            </div>
            <div v-else>
                <img
                    class="backdrop"
                    :src="
                        `https://image.tmdb.org/t/p/w780${infoObj.backdrop_path}`
                    "
                    alt=""
                />
            </div>

            <!-- Info -->
            <div class="info">{{ infoObj.overview }}</div>

            <i class="fas fa-times" @click="hideInfo"></i>
        </div>
    </main>
</template>

<script>
import Library from "@/components/Library.vue";

export default {
    name: "Content",
    components: {
        Library,
    },
    props: {
        filmsList: Array,
        seriesList: Array,
        popularList: Array,
        topRatedList: Array,
    },
    data() {
        return {
            screenOne: true,
            screenTwo: false,
            infoObj: {},
        };
    },
    methods: {
        showInfo(infoObj) {
            this.infoObj = infoObj;
            this.screenOne = false;
            this.screenTwo = true;
        },
        hideInfo() {
            this.screenOne = true;
            this.screenTwo = false;
        },
    },
};
</script>

<style lang="scss" scoped>
main {
    padding: 50px 0;

    .screenOne {
        h1 {
            color: #fff;
            padding: 30px 10px;
        }
        .cards {
            display: flex;
            overflow-x: auto;
            scrollbar-width: thin;
            scrollbar-color: #ff0000 #141414;
        }
    }

    .screenTwo.container {
        width: 780px;
        margin: 0 auto;
        color: #fff;
        position: relative;

        img {
            width: 780px;
            height: 439px;
            object-fit: cover;
        }

        .info {
            padding-top: 20px;
            line-height: 20px;
            text-align: center;
        }

        i {
            display: flex;
            justify-content: center;
            align-items: center;
            position: absolute;
            top: 20px;
            right: 20px;
            width: 40px;
            height: 40px;
            border-radius: 50%;
            background: #141414;
            font-size: 25px;
        }
    }
}
</style>
