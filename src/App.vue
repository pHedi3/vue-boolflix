<template>
  <div id="app">
    <Header @serch="takeSerch" />
    <Main :films="filterFilms" :usSerch="usSerch" />
  </div>
</template>

<script>
import axios from 'axios';
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
      textSerch: "",
      usSerch: false
    }
  },
  created() {
    axios.get('https://api.themoviedb.org/3/search/movie?api_key=098554c0b3206d5eb1f641f49f7c0115&query=ritorno+al+futuro').then((res) => {
      this.films = res.data.results
    })
  },
  computed: {
    filterFilms() {
      return this.films.filter((element) => {
        return element.title.toLowerCase().includes(this.textSerch.toLowerCase())
      })
    }
  },
  methods: {
    takeSerch(text) {
      this.usSerch = false
      this.textSerch = text
      if(text != "") {
        this.usSerch = true

      }
    }
  }
};
</script>

<style lang="scss">
@import "./style/app.scss";
#app {
  height: 100vh;
  background: linear-gradient(to top, #1c1c1c 10%, #1b1b1b);
  color: white;
}
</style>
