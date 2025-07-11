<script setup lang="ts">
import heroBackgroundImage from '@/assets/hero/mida-hero.webp';
</script>

<template>
  <section 
    id="hero" 
    class="hero" 
    :style="{ backgroundImage: `url(${heroBackgroundImage})` }"
  >
    <div class="hero__container">
      <h1 class="hero__title">MIDA - Food experience & catering</h1>
      <p class="hero__subtitle">
        MIDA es más que catering. Nuestro objetivo principal es brindarte una
        experiencia única, con sabores y aromas que te hagan sentir emociones.
        Nuestro equipo profesional está listo para crear contigo un menú que se
        ajuste a tus gustos, a tus necesidades y a tu presupuesto.
      </p>
    </div>
  </section>
</template>

<style lang="scss" scoped>
@use '@/styles/index.scss' as *;

.hero {
  // Layout y Dimensiones
  position: relative; // Necesario para el overlay
  display: flex;
  align-items: center;
  justify-content: center;
  min-height: 100vh; // Ocupa toda la altura de la pantalla
  padding: 0 5%;

  // Fondo
  background-size: cover;
  background-position: center center;
  background-attachment: fixed; // Efecto parallax sutil

  // Overlay oscuro para legibilidad. CRÍTICO para el diseño.
  &::before {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    // Usamos el color base oscuro con transparencia
    background: linear-gradient(180deg, rgba($MIDA-DARK, 0.4) 0%, rgba($MIDA-DARK, 0.7) 100%);
    z-index: 1;
  }

  &__container {
    position: relative; // Para que el contenido esté sobre el overlay
    z-index: 2;
    text-align: center;
    max-width: 800px; // Limita el ancho del texto para mejor lectura
    color: $MIDA-LIGHT;
  }

  &__title {
    font-family: var(--font-poppins);
    font-weight: 700;
    // Título responsive con clamp() para una fluidez perfecta
    font-size: clamp(2.5rem, 5vw, 4rem);
    line-height: 1.2;
    margin-bottom: 1.5rem;
    text-shadow: 0 2px 10px rgba($MIDA-DARK, 0.5);
  }

  &__subtitle {
    font-family: var(--font-poppins);
    font-weight: 300;
    font-size: clamp(1rem, 2.5vw, 1.25rem);
    line-height: 1.7;
    max-width: 650px; // Líneas más cortas son más fáciles de leer
    margin: 0 auto; // Centra el párrafo si es más angosto que el contenedor
    text-shadow: 0 2px 10px rgba($MIDA-DARK, 0.5);
  }

  // Ajustes para desktop
  @media (min-width: 768px) {
    justify-content: flex-start; // Alineamos a la izquierda en desktop

    &__container {
      text-align: left;
    }

    &__subtitle {
      margin: 0; // Quitamos el centrado automático
    }
  }
}
</style>