<template>
  <div>
    <div class="container">
      <div class="row">
        <h1>Films</h1>
        <Film class="col-3" v-for="film in films" :key="film.id" 
            :title="film.title"
            :orTitle="film.original_title"
            :orLen="film.original_language"
            :vote="film.vote_average"
            :poster_path="film.poster_path"
            :usSerch="usSerch"/>
      
      <h1>Series</h1>
          <Film class="col-3" v-for="serie in series" :key="serie.id" 
            :title="serie.name"
            :orTitle="serie.original_name"
            :orLen="serie.original_language"
            :vote="serie.vote_average"
            :poster_path="serie.poster_path"
            :usSerch="usSerch"/>
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
  props: {
      films: Array,
      series: Array,
      usSerch: Boolean
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
</style>