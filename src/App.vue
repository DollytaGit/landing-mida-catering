<script setup lang="ts">
import Footer from './components/globals/Footer.vue';
import Header from './components/globals/Header.vue';
import FloatingWhatsapp from './components/shared/FloatingWhatsapp.vue';

</script>

<template>
  <div class="header-container">
    <Header/>
  </div>
  <main class="main-content">
    <RouterView />
  </main>
  <Footer />
  <FloatingWhatsapp />
</template>


<style lang="scss">
@use '@/styles/index.scss' as *;

.main-content {
  min-height: 100vh;
}

.header-container {
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
