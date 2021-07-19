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
            <div class="star" v-for="(star, index) in stars" :key="index">
                <i v-show="star == 1" class="fas fa-star"></i>
                <i v-show="star == 0" class="far fa-star"></i>
            </div>
            <div v-if="this.falgOption.includes(this.orLen)">
              <img :src="createFlagPath" alt="" />
            </div>
            <div v-else>{{ createFlagPath }}</div>
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
            <div class="star" v-for="(star, index) in stars" :key="index">
                <i v-show="star == 1" class="fas fa-star"></i>
                <i v-show="star == 0" class="far fa-star"></i>
            </div>
          <div v-if="this.falgOption.includes(this.orLen)">
            <img :src="createFlagPath" alt="" />
          </div>
          <div v-else>{{ createFlagPath }}</div>
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
      falgOption: ["de", "en", "es", "fr", "it", "ja", "ko", "ru", "zh"],
      stars: []
    };
  },
  mounted() {
      this.genStar()
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
    createFlagPath() {
      if (this.falgOption.includes(this.orLen)) {
        return require("../assets/flag/" + this.orLen + ".svg");
      } else {
        return this.orLen;
      }
    },
  },
  methods: {
    timer() {
      this.hover = true;
      setTimeout(() => {
        this.hover = false;
      }, 3000);
    },
    genStar() {
        let int = parseInt( this.vote / 2)
        for (let x = 0; x < 5; x++) {
            if( x < int) {
                this.stars.push(1)
            } 
            if ( x <= 5 && x >= int) {
                this.stars.push(0)
            }
        }

    }
  },
};
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
    width: calc(100% - calc(var(--bs-gutter-x)));
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
      .star {
          display: inline-block;
          i {
              margin-right: 4px;
          }
      }
    }
  }
}
</style>