<template>
  <div class="Flag">
      <img v-if="orLen == 'de'" src="../assets/flag/de.svg" alt="">
      <img v-else-if="orLen == 'en'" src="../assets/flag/en.svg" alt="">
      <img v-else-if="orLen == 'es'" src="../assets/flag/es.svg" alt="">
      <img v-else-if="orLen == 'fr'" src="../assets/flag/fr.svg" alt="">
      <img v-else-if="orLen == 'it'" src="../assets/flag/it.svg" alt="">
      <img v-else-if="orLen == 'ja'" src="../assets/flag/ja.svg" alt="">
      <img v-else-if="orLen == 'ko'" src="../assets/flag/ko.svg" alt="">
      <img v-else-if="orLen == 'ru'" src="../assets/flag/ru.svg" alt="">
      <img v-else-if="orLen == 'zh'" src="../assets/flag/zh.svg" alt="">
      <div v-else>{{orLen}}</div>
  </div>
</template>

<script>
export default {
  name: "Falg",
  props: {
      orLen: String
  }


};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
img {
    height: 20px;
}
</style>