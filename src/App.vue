<template>
  <div id="app">
    <Header class="header" @serch="takeSerch" />
    <Main class="main" :films="films" :usSerch="usSerch" />
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
    this.takeSerch('a')

  },
  computed: {
  },
  methods: {
    filterFilms() {
      axios.get('https://api.themoviedb.org/3/search/movie?api_key=098554c0b3206d5eb1f641f49f7c0115&query=' + this.textSerch).then((res) => {
        this.films = res.data.results
    })
    },
    takeSerch(text) {
      this.usSerch = false
      this.textSerch = text
      if(text != "") {
        this.usSerch = true
      }
      this.filterFilms()
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
