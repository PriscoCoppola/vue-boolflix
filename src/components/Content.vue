<template>
    <main>
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
                />
            </div>

            <!-- Series -->
            <h1 v-show="seriesList.length !== 0">Series</h1>
            <div class="cards">
                <Library
                    v-for="series in seriesList"
                    :key="series.id"
                    :info="series"
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
                />
            </div>

            <!-- Top Rated -->
            <h1>Top Rated</h1>
            <div class="cards">
                <Library
                    v-for="topRated in topRatedList"
                    :key="topRated.id"
                    :info="topRated"
                />
            </div>
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
};
</script>

<style lang="scss" scoped>
main {
    padding: 50px 0;

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
</style>
