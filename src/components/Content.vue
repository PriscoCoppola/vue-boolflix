<template>
    <main>
        <div
            class="searchList"
            v-if="filmsList.length !== 0 || seriesList.length !== 0"
        >
            <h1>Series</h1>
            <div class="cards">
                <Library
                    v-for="film in filmsList"
                    :key="film.id"
                    :info="film"
                />
            </div>
            <h1>Movies</h1>
            <div class="cards">
                <Library
                    v-for="series in seriesList"
                    :key="series.id"
                    :info="series"
                />
            </div>
        </div>
        <div class="homepage" v-else>
            <h1>Popular</h1>
            <div class="cards">
                <Library
                    v-for="popular in popularList"
                    :key="popular.id"
                    :info="popular"
                />
            </div>
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
        padding: 10px;
    }
    .cards {
        display: flex;
        overflow-x: auto;
    }
}
</style>
