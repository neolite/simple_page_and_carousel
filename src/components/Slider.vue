<template>
<div class="block">
      <div class="level is-hidden-touch">
        <div class="level-left slider-control" @click="slidePrev">
          <arrow-left />
        </div>
        <div class="level-item" v-for="(img, idx) in viewImages" :key="idx">
          <figure class="image is-5by3">
            <img v-bind:src="img">
          </figure>
        </div>  
        <div class="level-right slider-control" @click="slideNext">
          <div class="block ">
            <arrow-right />
          </div>
        </div>
    </div>
      <div class="level is-hidden-desktop">
        <div class="level-left slider-control" @click="slidePrev">
          <arrow-left />
        </div>
        <div class="level-item">
          <figure class="image is-5by3">
            <img v-bind:src="images[this.currentIndex]">
          </figure>
        </div>  
        <div class="level-right slider-control" @click="slideNext">
          <div class="block ">
            <arrow-right />
          </div>
        </div>
    </div>
</div>

</template>
<script>
import ArrowRight from "vue-material-design-icons/arrow-right.vue";
import ArrowLeft from "vue-material-design-icons/arrow-left.vue";
export default {
  name: "Slider",
  props: ["images", "perPage"],
  components: {
    ArrowRight,
    ArrowLeft
  },
  computed: {
    viewImages() {
      return this.images.slice(
        this.currentIndex,
        this.currentIndex + this.imagesPerView
      );
    }
  },
  created() {
    this.imagesPerView = this.perPage;
  },
  data() {
    return {
      currentIndex: 0,
      imagesPerView: 3
    };
  },
  methods: {
    swipeStart() {
      console.log("swipeStart");
    },
    swipeMove() {
      console.log("swipeMove");
    },
    swipeEnd() {
      console.log("swipeEnd");
    },
    onTransitionEnd() {
      console.log("swipeEnd");
    },
    slidePrev() {
      if (this.currentIndex <= 0) return false;
      this.currentIndex--;
    },
    slideNext() {
      if (this.currentIndex >= this.images.length - this.perPage) return false;
      this.currentIndex++;
    }
  }
};
</script>
<style scoped>
.slider-control {
  cursor: pointer;
}
.image {
  padding: 4px;
}
</style>

