<template>
  <div>
    <div class="container">
      <div class="row">
        <h1>Films</h1>
        <div class="col-12 card-container">
        <Film class="card" v-for="(film, index) in films" :key="film.id" :id="index"
            :title="film.title"
            :orTitle="film.original_title"
            :orLen="film.original_language"
            :vote="film.vote_average"
            :poster_path="film.poster_path"
            :usSerch="usSerch"/>
            <div class="button" @click="goTo()"><i class="fas fa-arrow-right"></i></div>
        </div>
      <h1>Series</h1>
        <div  class="col-12 card-container">
          <Film  class="card" v-for="(serie, index) in series" :key="serie.id" :id="index"
            :title="serie.name"
            :orTitle="serie.original_name"
            :orLen="serie.original_language"
            :vote="serie.vote_average"
            :poster_path="serie.poster_path"
            :usSerch="usSerch"/>
            <div class="button"><i class="fas fa-arrow-right"></i></div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Film from "./Film.vue";
export default {
  name: "Main",
  components: {
    Film,
  },
  data() {
    return{
      curIndex: 4
    }
  },
  props: {
      films: Array,
      series: Array,
      usSerch: Boolean
  },
  methods: {
    goTo() {
      this.curIndex += 4
      document.getElementById(this.curIndex).scrollIntoView()
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.card-container {
  width: 100%;
  height: 400px;
  overflow: hidden;;
  position: relative;

  .card {
    width: calc(100% / 4 - 24px);
    display: inline-block;
    margin-right: 24px;
  }
  .button {
    display: flex;
    align-items: center;
    justify-content: center;
    height: 60px;
    width: 40px;
    font-size: 30px;
    position: absolute;
    top: 50%;
    left: 100%;
    transform: translate(-100%, -50%);
    background-color: rgba(0, 0, 0, 0.8);
  }
}
</style>