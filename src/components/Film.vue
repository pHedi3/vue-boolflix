<template>
  <div :style="'background-image: url(' + creatPathImg + ')'" class="mycard" @mouseover="hover = true" @mouseleave="hover = false">
    <div v-show="hoverCase" class="info-box">
      <div class="info">
        <div class="title">
          {{ title }}
        </div>
        <div class="more-info">
          {{ orTitle }}<br />
          <i v-for="n in 5" :key="n" class="fa-star" :class="genStar(n)"></i>
          <flag class="flag" :iso="fixLenguage" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: "Film",
  props: {
    title: String,
    orTitle: String,
    orLen: String,
    vote: Number,
    usSerch: Boolean,
    poster_path: String,
  },
  data() {
    return {
      hover: false,
    };
  },
  computed: {
    hoverSerch() {
      if (this.usSerch == true) {
        this.timer();
        return true;
      } else {
        return false;
      }
    },
    creatPathImg() {
      return "https://image.tmdb.org/t/p/w342" + this.poster_path;
    },
    fixLenguage() {
      if (this.orLen == 'en') {
        return 'us'
      } else {
        return this.orLen
      }
    },
    hoverCase() {
      if (this.poster_path == null) {
        return true
      } 
      if (this.hover) {
        return true
      }
      if (this.hoverSerch && this.hover) {
        return true
      }
      return false
    }
  },
  methods: {
    timer() {
      this.hover = true;
      setTimeout(() => {
        this.hover = false;
      }, 1500);
    },
    genStar(n) {
      let int = parseInt( this.vote / 2)
      if( n <= int) {
        return 'fas'
      } else  {
        return 'far'
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.mycard {
  background-position: center;
  background-size: cover;
  padding: 0;
  height: 400px;
  width: calc(25% - calc(var(--bs-gutter-x)) );
  .info-box {
    height: 100%;
    position: relative;
    background-color: rgba(0, 0, 0, .5);
    .info {
      width: 200px;
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      font-size: 18px;
      text-align: center;
      display: block;
      .title {
        font-size: 34px;
        font-weight: bold;
        margin-bottom: 8px;
      }
      i {
        display: inline-block;
        margin-right: 4px;
      }
      .flag {
        display: inline-block;
        width: 100%;
        height: 30px;
      }
    }
  }
}
</style>