<script setup>
const slides = ref([
  'https://swiperjs.com/demos/images/nature-1.jpg',
  'https://swiperjs.com/demos/images/nature-2.jpg',
  'https://swiperjs.com/demos/images/nature-3.jpg',
  'https://swiperjs.com/demos/images/nature-4.jpg',
  'https://swiperjs.com/demos/images/nature-5.jpg',
]);

const mainSwiper = ref(null);
const thumbsSwiper = ref(null);

const setSwiper = (swiper) => {
  mainSwiper.value = swiper;
};
const setThumbsSwiper = (swiper) => {
  thumbsSwiper.value = swiper;
};

const SwiperConfig = {
  modules: [
    SwiperEffectCreative,
    SwiperNavigation,
    SwiperThumbs,
    SwiperController,
  ],
  loop: true,
  effect: 'creative',
  slidesPerView: 1,
  watchSlidesProgress: true,
  navigation: {
    nextEl: '.swiper_controls_next',
    prevEl: '.swiper_controls_prev',
  },
  creativeEffect: {
    prev: {
      shadow: false,
      translate: ['-20%', 0, -1],
      scale: 0.9,
    },
    next: {
      translate: ['100%', 0, 0],
      scale: 0.8,
    },
  },
};
const SwiperThumbsConfig = {
  modules: [SwiperNavigation, SwiperThumbs, SwiperController],
  slidesPerView: slides.value.length,
  spaceBetween: 10,
  watchSlidesProgress: true,
  loop: false,
  followFinger: false,
};
</script>

<template>
  <div>
    <h1>Nuxt Swiper Basic Example</h1>
    <hr />
    <h2>Swiper Creative Effect</h2>
    <div class="swiper_wrapper">
      <Swiper
        :height="300"
        v-bind="SwiperConfig"
        :thumbs="{ swiper: thumbsSwiper }"
        @swiper="setSwiper"
        class="main-slider"
      >
        <SwiperSlide v-for="(slide, idx) in slides" :key="idx">
          <img :src="slide" />
        </SwiperSlide>
      </Swiper>
      <div class="swiper_controls">
        <div class="swiper_controls_prev"></div>
        <div class="swiper_controls_next"></div>
      </div>
    </div>
    <Swiper
      :height="300"
      v-bind="SwiperThumbsConfig"
      @swiper="setThumbsSwiper"
      class="thumbs"
    >
      <SwiperSlide v-for="(slide, idx) in slides" :key="idx">
        <img :src="slide" />
      </SwiperSlide>
    </Swiper>
  </div>
</template>

<style>
.swiper_wrapper {
  position: relative;
}
.swiper_controls {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: yellow;
  display: flex;
  align-items: stretch;
  justify-content: stretch;
  z-index: 10;
  background-color: transparent;
}
.swiper_controls div {
  flex-grow: 1;
}
.swiper_controls_prev {
  cursor: url(assets/btn-left.png) 64 64, pointer;
}
.swiper_controls_next {
  cursor: url(assets/btn-right.png) 64 64, pointer;
}
.swiper-slide {
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 18px;
  height: 400px;
  font-size: 4rem;
  font-weight: bold;
  font-family: 'Roboto', sans-serif;
}
.swiper-wrapper {
  min-width: 100vh;
  width: 100vh;
  transition-timing-function: ease-in;
}
.thumbs {
  margin-top: 10px;
  height: 100px;
}

.thumbs .swiper-slide {
  width: 25%;
  height: 100%;
  opacity: 0.3;
  cursor: pointer;
}

.thumbs .swiper-slide-thumb-active {
  opacity: 1;
}

.swiper-slide img {
  display: block;
  width: 100%;
  height: 100%;
  object-fit: cover;
}
</style>
