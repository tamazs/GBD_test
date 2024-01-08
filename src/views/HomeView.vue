<script setup>
import { ref, nextTick } from 'vue';
import { gsap } from 'gsap';
import Banner from '@/components/Banner.vue';
import Popup from '@/components/Popup.vue';
import staticBg from '@/assets/static_bg.png';

const showBanner = ref(true);
const showPopup = ref(false);

const handleBannerClose = async () => {
  await gsap.to('.banner', { y: '-100%', duration: 1 }).then(() => {
    showBanner.value = false;
    nextTick(() => {
      showPopup.value = true;
      animatePopupIn();
    });
  });
};

const handlePopupClose = () => {
  gsap.to('.popup', {
    scale: 0.5,
    opacity: 0,
    duration: 0.5,
    onComplete: () => {
      showPopup.value = false;
    },
  });
};

const animatePopupIn = () => {
  nextTick(() => {
    if (document.querySelector('.popup')) {
      gsap.fromTo('.popup', { scale: 0.5, opacity: 0 }, { scale: 1, opacity: 1, duration: 0.5 });
    }
  });
};
</script>

<template>
  <div class="home-container">
    <Banner v-if="showBanner" @close="handleBannerClose" />
    <Popup v-if="showPopup" @close="handlePopupClose" />
    <div class="bg-container">
      <img :src="staticBg" alt="Background image">
    </div>
  </div>
</template>

<style scoped lang="scss">
.home-container {
  font-family: 'Raleway', sans-serif;

  .bg-container {
    height: 100vh;
    width: 100vw;
    padding: 0;

    img {
      height: 100%;
      width: 100%;
    }
  }
}
</style>
