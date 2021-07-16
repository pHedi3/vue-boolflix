<template>
  <div class="film" @mouseover="hover = true" @mouseleave="hover = false">
    <img
      src="https://image.tmdb.org/t/p/w342/hQq8xZe5uLjFzSBt4LanNP7SQjl.jpg"
      alt=""
    />
    <div v-if="hover || (hoverSerch && hover )" class="info-box">
      <div class="info">
        <div class="title">
          {{ title }}
        </div>
        <div class="more-info">
          {{ orTitle }}<br />
          {{ orLen }}<br />
          {{ vote }}
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

  img {
    width: 100%;
  }
  .info-box {
    position: absolute;
    top: 0;
    left: 50%;
    transform: translate(-50%);

    background-color: rgba(0, 0, 0, 0.5);
    height: 100%;
    width: calc(100% - calc(var(--bs-gutter-x)));
    .info {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      font-size: 10px;
      text-align: center;
      display: block;
      .title {
        font-size: 14px;
        font-weight: bold;
        margin-bottom: 12px;
      }
    }
  }
}
</style>