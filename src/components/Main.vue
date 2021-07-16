<template>
  <div class="main">
    <div class="container">
      <div class="row">
        <Film class="col-2" v-for="film in films" :key="film.id" 
            :title="film.title"
            :orTitle="film.original_title"
            :orLen="film.original_language"
            :vote="film.vote_average"
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
      usSerch: Boolean
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
</style>