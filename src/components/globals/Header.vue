<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue';

// --- Estado Reactivo ---

// Controla si el usuario ha hecho scroll hacia abajo
const isScrolled = ref(false);
// Controla la visibilidad del menú en móviles
const isMobileMenuOpen = ref(false);

// --- Lógica del Componente ---

/**
 * Maneja el evento de scroll para actualizar el estado del header.
 * Se activa si el scroll vertical es mayor a 20px.
 */
const handleScroll = () => {
  isScrolled.value = window.scrollY > 20;
};

/**
 * Alterna la visibilidad del menú móvil.
 */
const toggleMobileMenu = () => {
  isMobileMenuOpen.value = !isMobileMenuOpen.value;
};

// --- Ciclo de Vida ---

// Añadimos el listener cuando el componente se monta en el DOM
onMounted(() => {
  window.addEventListener('scroll', handleScroll);
});

// Es CRUCIAL limpiar el listener cuando el componente se destruye para evitar memory leaks
onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll);
});
</script>

<template>
  <header
    class="header"
    :class="{
      'scrolled': isScrolled,
      'mobile-menu-open': isMobileMenuOpen
    }"
  >
    <div class="header__container">
      <a href="/" class="header__logo" aria-label="MIDA Catering - Inicio">
        MIDA
      </a>

      <button
        class="header__mobile-toggle"
        @click="toggleMobileMenu"
        aria-label="Abrir menú"
        :aria-expanded="isMobileMenuOpen"
      >
        <span class="header__mobile-toggle-bar"></span>
        <span class="header__mobile-toggle-bar"></span>
        <span class="header__mobile-toggle-bar"></span>
      </button>

      <nav class="header__nav">
        <ul class="header__nav-list">
          <li class="header__nav-item">
            <a href="#catering" @click="isMobileMenuOpen = false">Catering</a>
          </li>
          <li class="header__nav-item">
            <a href="#contacto" @click="isMobileMenuOpen = false">Contacto</a>
          </li>
        </ul>
      </nav>

      <a href="https://instagram.com" target="_blank" rel="noopener noreferrer" class="header__social-icon" aria-label="Visita nuestro Instagram">
        <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
          <rect x="2" y="2" width="20" height="20" rx="5" ry="5"></rect>
          <path d="M16 11.37A4 4 0 1 1 12.63 8 4 4 0 0 1 16 11.37z"></path>
          <line x1="17.5" y1="6.5" x2="17.51" y2="6.5"></line>
        </svg>
      </a>
    </div>
  </header>
</template>

<style lang="scss" scoped>
@use '@/styles/index.scss' as *;

.header {
  // Posicionamiento y layout
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  z-index: 1000;
  padding: 1.5rem 5%; // Padding responsive
  background-color: transparent;

  // Transiciones para un efecto suave y "caro"
  transition: background-color 0.4s ease, box-shadow 0.4s ease, padding 0.4s ease;

  // Estilos del texto y logo por defecto
  color: $MIDA-LIGHT;

  &__container {
    display: flex;
    justify-content: space-between;
    align-items: center;
    width: 100%;
    margin: 0 auto;
    max-width: 1400px; // Un max-width para layouts grandes
  }

  &__logo {
    font-family: var(--font-titillium); // Titillium o una fuente serif da un toque elegante
    font-weight: 600;
    font-size: 2rem;
    text-decoration: none;
    color: inherit; // Hereda el color del padre (.header)
    transition: color 0.4s ease;
  }

  // --- Estilos Mobile First ---

  &__mobile-toggle {
    display: flex; // Visible por defecto en móvil
    flex-direction: column;
    justify-content: space-around;
    width: 2rem;
    height: 2rem;
    background: transparent;
    border: none;
    cursor: pointer;
    padding: 0;
    z-index: 10;

    &-bar {
      width: 2rem;
      height: 0.25rem;
      background: $MIDA-LIGHT;
      border-radius: 10px;
      transition: all 0.3s linear;
      position: relative;
      transform-origin: 1px;
    }
  }

  &__nav {
    display: flex;
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100vh;
    background-color: $MIDA-DARK;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    transform: translateX(100%);
    transition: transform 0.4s ease-in-out;
  }

  &__nav-list {
    list-style: none;
    padding: 0;
    margin: 0;
    text-align: center;
  }

  &__nav-item {
    margin: 2rem 0;

    a {
      font-family: var(--font-poppins);
      font-size: 1.5rem;
      font-weight: 500;
      color: $MIDA-LIGHT;
      text-decoration: none;
      transition: color 0.3s ease;

      &:hover {
        color: $MIDA-GREEN;
      }
    }
  }

  &__social-icon {
    display: none; // Oculto en móvil para simplicidad, visible en desktop
    color: inherit;
    transition: color 0.4s ease;
  }

  // --- Estado Scrolled ---

  &.scrolled {
    background-color: $MIDA-LIGHT;
    color: $MIDA-DARK; // Cambia el color para todos los hijos
    padding: 1rem 5%;
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.05);

    .header__mobile-toggle-bar {
      background: $MIDA-DARK;
    }
  }

  // --- Estado Menú Móvil Abierto ---
  &.mobile-menu-open {
    .header__nav {
      transform: translateX(0);
    }

    // Animación de la hamburguesa a una "X"
    .header__mobile-toggle-bar:nth-child(1) {
      transform: rotate(45deg);
    }

    .header__mobile-toggle-bar:nth-child(2) {
      opacity: 0;
      transform: translateX(20px);
    }

    .header__mobile-toggle-bar:nth-child(3) {
      transform: rotate(-45deg);
    }
  }

  // --- Media Query para Desktop (Tablet y más grandes) ---

  @media (min-width: 768px) {
    &__mobile-toggle {
      display: none; // Ocultamos la hamburguesa
    }

    &__nav {
      // Devolvemos el nav a su estado normal
      position: static;
      height: auto;
      width: auto;
      background-color: transparent;
      transform: translateX(0);
      flex-direction: row;
      transition: none;
    }

    &__nav-list {
      display: flex;
      flex-direction: row;
      gap: 2.5rem; // Espacio entre items
    }

    &__nav-item {
      margin: 0;

      a {
        font-size: 1rem;
        // Hereda el color (blanco/negro) del header
        color: inherit;

        &:hover {
          color: $MIDA-GREEN;
        }
      }
    }

    &__social-icon {
      display: block; // Mostramos el icono de Instagram
    }
  }
}
</style>