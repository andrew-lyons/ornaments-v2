<template>
  <div>
    <carousel
      :perPage="1"
      :autoplay="true"
      :loop="true"
      :navigationEnabed="true"
    >
      <slide>
        <img width="375" :src="img[0]" alt="">
      </slide>
      <slide>
        <ik-image width="375" :path="img[1]"></ik-image>
      </slide>
      <slide>
        <ik-image width="375" :path="img[2]"></ik-image>
      </slide>
    </carousel>
  </div>
</template>

<script>
import { Carousel, Slide } from 'vue-carousel';
import ImageKit from "imagekitio-vue"
import Vue from 'vue'

Vue.use(ImageKit, {
  urlEndpoint: "https://ik.imagekit.io/5mrrpg2bgjs/"
})

export default {
    name: 'ImageCarousel',
    components: {
        Carousel,
        Slide
    },
    props: {
        img: { type: Array, required: true }
    }
}
</script>