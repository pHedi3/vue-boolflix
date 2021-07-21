<template>
  <div class="film" @mouseover="hover = true" @mouseleave="hover = false">
    <img v-if="poster_path != null" :src="creatPathImg" alt="" />
    <div v-else class="incase">
      <div class="info-box">
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
    <div v-if="(hover || (hoverSerch && hover)) && poster_path != null" class="info-box">
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
    }
  },
  methods: {
    timer() {
      this.hover = true;
      setTimeout(() => {
        this.hover = false;
      }, 3000);
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
.film {
  position: relative;
  margin-bottom: 24px;
  img {
    width: 100%;
  }
  .incase {
    height: 390px;
  }
  .info-box {
    position: absolute;
    top: 0;
    left: 50%;
    transform: translate(-50%);
    background-color: rgba(0, 0, 0, 0.3);
    height: 100%;
    width: 100%;
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
      img {
        height: 30px;
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