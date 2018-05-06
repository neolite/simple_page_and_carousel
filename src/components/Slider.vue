<template>
<div class="block">
      <div class="level is-hidden-touch">
        <div class="level-left slider-control" @click="slidePrev">
          <arrow-left />
        </div>
        <div class="level-item" >
          <div class="columns">
            <div class="column" v-for="(img, idx) in viewImages" :key="idx">
              <figure class="image is-320x240">
                <img class="is-3by2" :src="img" @click="slideTo(idx, viewImages.length)">
              </figure>
            </div>
          </div>
        </div>  
        <div class="level-right slider-control" @click="() => slideNext(imagesPerView)">
          <div class="block ">
            <arrow-right :disabled="currentIndex===images.length"/>
          </div>
        </div>
    </div>
    <div class="level is-hidden-touch">
      <div class="level-item" >
          <nav class="pagination is-rounded is-centered" role="navigation" aria-label="pagination">
            <ul class="pagination-list">
              <li :key="idx" v-for="(image, idx) in viewImages">
                <a v-if="idx===currentBlock" @click="() => currentIndex=(idx*perPage)" class="pagination-link is-current" aria-current="page"></a>
                <a v-else @click="() => currentIndex=(idx*perPage)"  class="pagination-link"></a>
                </li>
            </ul>
          </nav>
      </div>
    </div>
      <div class="level is-hidden-desktop">
        <div class="level-item">
          <figure 
            class="image is-320x240"  
            v-touch:swipe.left="() => slideNext(1)"
            v-touch:swipe.right="slidePrev">
            <img v-bind:src="images[this.currentIndex]">
          </figure>
        </div>
        <div class="level-end">
          <nav class="pagination is-rounded is-centered" role="navigation" aria-label="pagination">
            <ul class="pagination-list">
              <li :key="idx" v-for="(image, idx) in images">
                <a v-if="idx===currentIndex" @click="() => currentIndex=idx" class="pagination-link is-current" aria-current="page"></a>
                <a v-else @click="() => currentIndex=idx"  class="pagination-link"></a>
                </li>
            </ul>
          </nav>
        </div>
    </div>
</div>

</template>
<script>
import Vue from "vue";
import Vue2TouchEvents from "vue2-touch-events";

import ArrowRight from "vue-material-design-icons/arrow-right.vue";
import ArrowLeft from "vue-material-design-icons/arrow-left.vue";

Vue.use(Vue2TouchEvents);

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
    },
    currentBlock() {
      return Math.round(
        this.currentIndex / (this.images.length / this.imagesPerView)
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
    slideTo(idx, length) {
      if (idx === 0 && this.currentIndex > 0) {
        this.currentIndex--;
      }
      if (
        idx === length - 1 &&
        this.currentIndex + this.perPage < this.images.length
      ) {
        this.currentIndex++;
      }
    },
    slidePrev() {
      if (this.currentIndex <= 0) return false;
      this.currentIndex--;
    },
    slideNext(perPage = null) {
      const imagePerPage = perPage ? perPage : this.perPage;
      if (this.currentIndex >= this.images.length - imagePerPage) return false;
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
  padding-right: 4px;
}
</style>
