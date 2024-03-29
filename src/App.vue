<template>
  <div>
    <transition name="fade" mode="out-in" enter-active-class="animate__animated animate__fadeIn animate__faster"
      leave-active-class="animate__animated animate__fadeOut animate__faster">
      <loading v-if="isLoading" />
      <div v-else class="position-relative">
        <Navbar />
        <HamburgerMenuNavbar />
        <router-view />
        <Footer />
        <div @click="scrollToTop"
          class="scroll-to-top-button bg-artrodite rounded-circle text-center d-flex align-items-center justify-content-center"
          style="width: 40px; height: 40px;">
          <i class="fa-solid fa-chevron-up fs-6"></i>
        </div>
      </div>
    </transition>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import Navbar from '@/components/Navbar.vue';
import HamburgerMenuNavbar from '@/components/HamburgerMenuNavbar'
import Loading from '@/components/Loading.vue';
import Footer from '@/components/Footer.vue';
import { onMounted, watch } from '@vue/runtime-core';
import { useRoute } from 'vue-router'
import AOS from 'aos'
import 'aos/dist/aos.css'

onMounted(() => {
  AOS.init({
    duration: 1000,
    once: false,
    dataAosOut: 'fade-out'
  })
})

const route = useRoute()

watch(() => route.path, () => {
  scrollToTop()
})

const isLoading = ref(true);
onMounted(() => {
  setTimeout(() => {
    isLoading.value = false;
  }, 1000)
})

const scrollToTop = () => {
  window.scrollTo({
    top: 0,
    behavior: 'smooth'
  })
}
</script>

<style lang="scss">
@import './css/_animation.scss';
@import '~bootstrap/dist/css/bootstrap.css';

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'Satoshi-Variable', sans-serif;
  background: #F1F1F1;
  overflow-x: hidden;
  font-size: 20px;
  font-weight: 500;
}

body > div {
  overflow-x:hidden;
}

@media (min-width: 768px) {
  ::selection {
    color: #F1F1F1;
    background: #070707;
  }

  ::-webkit-scrollbar-track {
    background-color: #F3F3F3;
  }

  ::-webkit-scrollbar {
    width: 2px;
    background-color: #F3F3F3;
  }

  ::-webkit-scrollbar-thumb {
    background-color: #070707;
  }
}

a {
  color: #000;
  text-decoration: none;
}

.scroll-to-top-button {
  position: fixed;
  bottom: 50px;
  right: 20px;
  color: #000;
  cursor: pointer;
  font-size: 24px;
}

.sticky-top {
  z-index: 1;
}</style>
