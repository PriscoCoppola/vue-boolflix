<template>
    <div id="app">
        <Header @performSearch="getLibrary"/>

        <main>
            <Content :filmsList="films" />
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
        films: [],
      }
    },
    methods: {
      getLibrary(search) {
            Promise.all([axios.get("https://api.themoviedb.org/3/search/movie?api_key=b91b4dc2e6d19b04fe76e513e83a3219&language=it-IT&query=" + search), axios.get("https://api.themoviedb.org/3/search/tv?api_key=e99307154c6dfb0b4750f6603256716d&language=it-IT&query=" + search)])
                .then((res) => {
                  const films = res[0].data.results
                  const series = res[1].data.results

                  let library = [...films, ...series]
                  this.films = library
                  console.log(films);
                  })
                .catch((err) => {
                    console.log("Error", err);
                });
        },
    }
};
</script>

<style lang="scss">
@import url(https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.3/css/all.min.css);
@import "@/styles/general.scss";


</style>
