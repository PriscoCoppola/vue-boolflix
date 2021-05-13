<template>
    <div id="app">
        <Header @performSearch="getLibrary" />

        <Content
            :filmsList="films"
            :seriesList="series"
            :popularList="popularList"
            :topRatedList="topRatedList"
        />
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
                .get(this.apiURL + "search/movie", {
                    params: {
                        api_key: "b91b4dc2e6d19b04fe76e513e83a3219",
                        language: "it-IT",
                        query: search,
                    },
                })
                .then((res) => {
                    this.films = res.data.results;
                });
            // Search Series API
            axios
                .get(this.apiURL + "search/tv", {
                    params: {
                        api_key: "b91b4dc2e6d19b04fe76e513e83a3219",
                        language: "it-IT",
                        query: search,
                    },
                })
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
