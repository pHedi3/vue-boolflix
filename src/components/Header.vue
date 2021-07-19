<template>
  <div>
    <div class="right">
      <img src="../assets/Netflix_logo.svg" alt="" />
      <ul>
        <li>Home</li>
        <li>Serie TV</li>
        <li>Film</li>
        <li>Originali</li>
        <li>Aggiunti di recente</li>
        <li>La mia lista</li>
      </ul>
    </div>
    <div class="left">
      <i @click="$emit('serch', serch)" class="fas fa-search"></i>
      <input type="text" placeholder="Cerca" v-model="serch" @keyup.enter="$emit('serch', serch)">
      <i class="fas fa-bell"></i>
      <i class="fas fa-user"></i>
      <i class="fas fa-sort-down"></i>
    </div>
  </div>
</template>

<script>
export default {
  name: "Header",
  data() {
    return {
      serch: ""
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
  .right {
    display: flex;
    align-items: center;
    ul {
      margin: 0 24px;
      padding: 0;
      display: flex;
      align-items: center;
      list-style: none;
      li {
        margin-right: 12px;
        color: #bbb;
        &:hover {
          color: white;
        }
      }
    }
    img {
      height: 100%;
    }
  }
  .left {
    display: flex;
    align-items: center;
    i {
      display: inline;
      font-size: 18px;
      margin-left: 12px;
      cursor: pointer;
      &:last-of-type {
        font-size: 12px;
        margin-left: 6px;
        vertical-align: top;
      }
    }
    input {
      margin-left: 12px;
      background-color: #1b1b1b;
      border: none;
      color: white;
    }
  }
</style>
