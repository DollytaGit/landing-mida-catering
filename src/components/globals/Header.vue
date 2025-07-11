<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue';
import logo from '@/assets/logos/mida-logo.webp';

// --- Estado y Lógica para el efecto de scroll ---
const isScrolled = ref(false);

const handleScroll = () => {
  isScrolled.value = window.scrollY > 20;
};

onMounted(() => {
  window.addEventListener('scroll', handleScroll, { passive: true });
});

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll);
});
</script>

<template>
  <header class="header" :class="{ 'scrolled': isScrolled }">
    <div class="header__content-wrapper">
      <figure class="header__logo-container">
        <router-link to="/" class="header__logo">
          <img :src="logo" alt="MIDA Logo">
        </router-link>
      </figure>

      <div class="header__social">
        <a href="https://instagram.com" target="_blank" rel="noopener noreferrer" aria-label="Visita nuestro Instagram">
          <i class="fa-brands fa-instagram"></i>
        </a>
      </div>
    </div>
  </header>
</template>

<style lang="scss" scoped>
@use '@/styles/index.scss' as *;

// --- Estilos para el CONTENEDOR EXTERNO ---
.header {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  padding: 1.5rem 5%; // Padding de seguridad para los lados
  z-index: 1000;

  background-color: transparent;
  color: $MIDA-LIGHT;
  transition: background-color 0.4s ease, box-shadow 0.4s ease, padding 0.4s ease;

  &.scrolled {
    background-color: $MIDA-LIGHT;
    color: $MIDA-DARK;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.07);
    padding: 1rem 5%;
  }
}

// --- Estilos para el NUEVO CONTENEDOR INTERNO ---
.header__content-wrapper {
  // Centrado y con ancho máximo
  width: 100%;
  max-width: 1440px; // El ancho máximo de tu contenido
  margin: 0 auto; // La clave para centrar el bloque

  // El Flexbox se aplica aquí ahora
  display: flex;
  justify-content: space-between;
  align-items: center;
}

// --- Estilos para el contenido (sin apenas cambios) ---

.header__logo-container {
  margin: 0;
  padding: 0;
  display: flex;
}

.header__logo {
  img {
    display: block;
    height: 40px;
    width: auto;
    transition: height 0.4s ease;
  }
}

.scrolled .header__logo img {
  height: 35px;
}

.header__social {

  position: relative;
  right: 3rem;

  a {
    display: block;
    color: inherit;
    transition: color 0.3s ease;

    &:hover {
      color: $MIDA-GREEN;
    }

    i {
      font-size: 1.75rem;
      vertical-align: middle;
    }
  }

  @media(min-width: 768px) {
    right: 5rem;
  }
}
</style>