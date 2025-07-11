<script setup lang="ts">
import Footer from './components/globals/Footer.vue';
import Header from './components/globals/Header.vue';

</script>

<template>
  <Header/>
  <main>
    <RouterView />
  </main>
  <Footer />
</template>


<style lang="scss">
@use '@/styles/index.scss' as *;

.main-content {
  min-height: 100vh;
}

.main-content.with-header {
  margin-top: 56px;
}
</style>
