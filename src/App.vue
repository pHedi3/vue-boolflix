<template>
  <div id="app">
    <Header class="header" @serch="[takeSerch($event), filterFilms(), filterSeries()]" />
    <Main class="main" :series="listSeries" :films="listFilm" :usSerch="usSerch" />
  </div>
</template>

<script>
import axios from "axios";
import Header from "./components/Header.vue";
import Main from "./components/Main.vue";

export default {
  name: "App",
  components: {
    Header,
    Main,
  },
  data() {
    return {
      films: [],
      series: [],
      listFilm: [],
      listSeries: [],
      textSerch: "",
      usSerch: false,
    };
  },
  created() {
    axios.get("https://api.themoviedb.org/3/movie/popular?api_key=098554c0b3206d5eb1f641f49f7c0115&language=en-US&page=1")
      .then((res) => {
        this.films = res.data.results;
        this.listFilm = this.films;
      });
    axios.get("https://api.themoviedb.org/3/tv/popular?api_key=098554c0b3206d5eb1f641f49f7c0115&language=en-US&page=1")
      .then((res) => {
        this.series = res.data.results;
        this.listSeries = this.series;
      });
  },
  methods: {
    filterFilms() {
      if(this.takeSerch != "") {
        axios.get("https://api.themoviedb.org/3/search/movie?api_key=098554c0b3206d5eb1f641f49f7c0115&query=" + this.textSerch)
          .then((res) => {
            this.listFilm = res.data.results;
          });
      } else {
        this.listFilm = this.films
      }
    },
    filterSeries() {
      if(this.takeSerch != "") {
        axios.get("https://api.themoviedb.org/3/search/tv?api_key=098554c0b3206d5eb1f641f49f7c0115&query=" + this.textSerch)
          .then((res) => {
            this.listSeries = res.data.results;
          });
      } else {
        this.listSeries = this.series
      }
    },
    takeSerch(text) {
      this.usSerch = false;
      this.textSerch = text;
      if (text != "") {
        this.usSerch = true;
      }
    }
  }
}
</script>

<style lang="scss">
@import "./style/app.scss";
#app {
  height: 100vh;
  background: linear-gradient(to top, #1c1c1c 10%, #1b1b1b);
  color: white;
  .header {
    display: flex;
    justify-content: space-between;
    height: 60px;
    padding: 12px 24px;
    font-size: 14px;
  }
  .main {
    height: calc(100% - 60px);
    overflow-y: auto;
  }
}
</style>