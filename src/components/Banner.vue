<template>
    <div v-show="showBanner" class="banner">
        <img :src="bannerImg" alt="New features available" class="banner-img" />
        <div class="banner-content">
            <h2>New features available!</h2>
            <p>Lorem Ipsum is simply dummy text of the printing and typesetting industry.</p>
            <button class="features-btn" @click="handleViewFeatures">View New Features</button>
        </div>
        <button class="close-btn" @click="closeBanner">
            <i class="fas fa-x"></i>
        </button>
    </div>
</template>
  
<script setup>
import { ref, onMounted, defineEmits } from 'vue';
import { gsap } from 'gsap';
import bannerImg from '@/assets/banner_img.png';

const showBanner = ref(false);
const emit = defineEmits(['close']);

onMounted(() => {
    setTimeout(() => {
        showBanner.value = true;
        gsap.fromTo('.banner', { y: '-100%' }, { duration: 1, y: 0 });
    }, 10000);
});

const closeBanner = () => {
    gsap.to('.banner', {
        duration: 1,
        y: '-100%',
        onComplete: () => {
            showBanner.value = false;
        },
    });
};

const handleViewFeatures = () => {
    closeBanner();
    emit('close');
};
</script>
  
<style lang="scss" scoped>
.banner {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    background-color: #ffffff;
    z-index: 10;
    padding: 1rem 6rem;
    box-sizing: border-box;
    display: flex;
    justify-content: center;
    gap: 7rem;
    align-items: center;
    transform: translateY(-100%);
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    background: radial-gradient(circle at 26rem, #26D1B0 0, #266ED1 40%);
}

.banner-img {
    height: auto;
    max-width: 20%;
    align-self: flex-start;
}

.banner-content {
    max-width: 70%;
    text-align: left;
    color: white;

    h2 {
        margin: 0;
        font-size: 3rem;
    }

    p {
        margin: 0.5rem 0;
        font-size: 1rem;
    }
}

.features-btn {
    background-color: rgba(255, 255, 255, 0.4);
    color: white;
    border: none;
    padding: 10px 20px;
    border-radius: 10px;
    cursor: pointer;
    font-size: 1rem;
    margin-top: 10px;
}

.close-btn {
    position: absolute;
    top: 1rem;
    right: 1rem;
    background: none;
    border: none;
    cursor: pointer;
    font-size: 1.5rem;
    color: white;
}

.fas.fa-x {
    font-size: 1.3rem;
    opacity: 64%;
}
</style>
  