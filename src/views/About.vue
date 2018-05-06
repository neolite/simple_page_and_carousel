<template>
<div>
  <div class="tile">
    <article>
      <h1>This is an about page</h1>
    </article>
  </div>
  <slider :images="images" :per-page="3"/>
</div>  
</template>
<script>
import Slider from "@/components/Slider";

export default {
  components: {
    Slider
  },
  data() {
    return {
      images: [
        "https://picsum.photos/320/240?image=1",
        "https://picsum.photos/320/240?image=2",
        "https://picsum.photos/320/240?image=3",
        "https://picsum.photos/320/240?image=4",
        "https://picsum.photos/320/240?image=5",
        "https://picsum.photos/320/240?image=6",
        "https://picsum.photos/320/240?image=7",
        "https://picsum.photos/320/240?image=8",
        "https://picsum.photos/320/240?image=9"
      ]
    };
  }
};
</script>
