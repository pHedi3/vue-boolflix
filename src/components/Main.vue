<template>
  <div>
    <div class="container">
      <div class="row">
        <h1>Films</h1>
        <div class="col-12 film card-container">
          <div class="row">
            <Film class="col-3" v-for="film in stampFilm" :key="film.id" 
            :title="film.title"
            :orTitle="film.original_title"
            :orLen="film.original_language"
            :vote="film.vote_average"
            :poster_path="film.poster_path"
            :usSerch="usSerch"/>
          </div>
          <div v-show="curIndexFilms >= 4" class="button-left" @click="goBackFilms()"><i class="fas fa-arrow-left"></i></div>
          <div v-show="curIndexFilms < films.length - 4" class="button-right" @click="goToFilms()"><i class="fas fa-arrow-right"></i></div>
        </div>
      <h1>Series</h1>
        <div  class="col-12 series card-container">
          <div class="row">
          <Film class="col-3" v-for="serie in stampSeries" :key="serie.id"
            :title="serie.name"
            :orTitle="serie.original_name"
            :orLen="serie.original_language"
            :vote="serie.vote_average"
            :poster_path="serie.poster_path"
            :usSerch="usSerch"/>
          </div>
          <div v-show="curIndexSeries >= 4" class="button-left" @click="goBackSeries()"><i class="fas fa-arrow-left"></i></div>
          <div v-show="curIndexSeries < series.length - 4" class="button-right" @click="goToSeries()"><i class="fas fa-arrow-right"></i></div>
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
      curIndexFilms: 0,
      curIndexSeries: 0
    }
  },
  props: {
      films: Array,
      series: Array,
      usSerch: Boolean
  },
  computed: {
    startFilm() {
      this.reset()
      return this.films
    },
    startSeries() {
      this.reset()
      return this.series
    },
    stampFilm() {
      return this.startFilm.slice(this.curIndexFilms, (this.curIndexFilms + 4))
    },
    stampSeries() {
      return this.startSeries.slice(this.curIndexSeries, (this.curIndexSeries + 4))
    }
  },
  methods: {
    reset() {
      this.curIndexSeries = 0
      this.curIndexFilms = 0
    },
    goToFilms() {
      this.curIndexFilms += 4
    },
    goToSeries() {
      this.curIndexSeries += 4
    },
    goBackFilms() {
      this.curIndexFilms -= 4
    },
    goBackSeries() {
      this.curIndexSeries -= 4
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.card-container {
  width: 100%;
  display: flex;
  align-items: center;
  position: relative;
  .button-left {
    display: flex;
    align-items: center;
    justify-content: center;
    height: 200px;
    width: 40px;
    font-size: 30px;
    position: absolute;
    top: 50%;
    left: calc(0% + calc(var(--bs-gutter-x)* .5));
    transform: translate(0, -50%);
    background-color: rgba(0, 0, 0, 0.8);

  }

  .button-right {
    display: flex;
    align-items: center;
    justify-content: center;
    height: 200px;
    width: 40px;
    font-size: 30px;
    position: absolute;
    top: 50%;
    left: calc(100% - calc(var(--bs-gutter-x)* .5));
    transform: translate(-100%, -50%);
    background-color: rgba(0, 0, 0, 0.8);
  }
}
</style>