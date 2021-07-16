<template>
  <div class="film" @mouseover="hover = true" @mouseleave="hover = false">
    <img v-if="poster_path != null"
      :src="creatPathImg"
      alt=""
    />
    <div v-else>
        <div class="info-box">
      <div class="info">
        <div class="title">
          {{ title }}
        </div>
        <div class="more-info">
          {{ orTitle }}<br />
          {{ vote }}
          <Flag :orLen="orLen" />
        </div>
      </div>
    </div>
    </div>
    <div v-if="hover || (hoverSerch && hover )" class="info-box">
      <div class="info">
        <div class="title">
          {{ title }}
        </div>
        <div class="more-info">
          {{ orTitle }}<br />
          {{ vote }}
          <Flag :orLen="orLen" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Flag from "./Flag.vue"
export default {
  name: "Film",
  components: {
      Flag
  },
  props: {
    title: String,
    orTitle: String,
    orLen: String,
    vote: Number,
    usSerch: Boolean,
    poster_path: String
  },
  data() {
    return {
      hover: false,
    };
  },
  computed: {
      hoverSerch() {
          if(this.usSerch == true) {
              this.timer()
              return true
          } else {
              return false
          }
      },
      creatPathImg() {
              return  'https://image.tmdb.org/t/p/w342' + this.poster_path
      }
  },
  methods: {
      timer() {
          this.hover = true
          setTimeout(() => {
              this.hover = false
          }, 3000);
      }

  }
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
      font-size: 16px;
      text-align: center;
      display: block;
      .title {
        font-size: 26px;
        font-weight: bold;
        margin-bottom: 12px;
      }
    }
  }
}
</style>