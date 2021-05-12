<template>
    <div id="app">
        <Header @performSearch="getLibrary" />

        <main>
            <Content
                :filmsList="films"
                :seriesList="series"
                :popularList="popularList"
                :topRatedList="topRatedList"
            />
        </main>
    </div>
</template>

<script>
import axios from "axios";

import Header from "@/components/Header.vue";
import Content from "@/components/Content.vue";

export default {
    name: "App",
    components: {
        Header,
        Content,
    },
    data() {
        return {
            apiURL: "https://api.themoviedb.org/3/",
            films: [],
            series: [],
            popularList: [],
            topRatedList: [],
        };
    },
    created() {
        // Popular API
        axios
            .get(this.apiURL + "movie/popular", {
                params: {
                    api_key: "b91b4dc2e6d19b04fe76e513e83a3219",
                    language: "it-IT",
                },
            })
            .then((res) => {
                this.popularList = res.data.results;
            });
        // Top Rated API
        axios
            .get(this.apiURL + "movie/top_rated", {
                params: {
                    api_key: "b91b4dc2e6d19b04fe76e513e83a3219",
                    language: "it-IT",
                },
            })
            .then((res) => {
                this.topRatedList = res.data.results;
            });
    },
    methods: {
        getLibrary(search) {
            // Search Film API
            axios
                .get(
                    "https://api.themoviedb.org/3/search/movie?api_key=b91b4dc2e6d19b04fe76e513e83a3219&language=it-IT&query=" +
                        search
                )
                .then((res) => {
                    this.films = res.data.results;
                });
            // Search Series API
            axios
                .get(
                    "https://api.themoviedb.org/3/search/tv?api_key=e99307154c6dfb0b4750f6603256716d&language=it-IT&query=" +
                        search
                )
                .then((res) => {
                    this.series = res.data.results;
                });
        },
    },
};
</script>

<style lang="scss">
@import url(https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.3/css/all.min.css);
@import "@/styles/general.scss";
</style>
