<script setup lang="ts">
import contactBgImage from '@/assets/contact/contact-img.webp';
const emailAddress = 'contacto@mida.com.ec';
</script>

<template>
  <section
    id="contacto"
    class="contact-section"
    :style="{ backgroundImage: `url(${contactBgImage})` }"
  >
    <div class="contact-section__container">
      <h2 class="contact-section__title">CONTACTO</h2>
      <p class="contact-section__subtitle">
        ¡Estamos ansiosos por escucharte! No dudes en ponerte en contacto con nosotros.
      </p>
      <a :href="`mailto:${emailAddress}`" class="contact-section__email">
        {{ emailAddress }}
      </a>
    </div>
  </section>
</template>

<style lang="scss" scoped>
@use '@/styles/index.scss' as *;

.contact-section {
  position: relative;
  padding: 6rem 5%;
  min-height: 60vh; // Una altura considerable pero menor que el Hero

  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;

  background-size: cover;
  background-position: center;
  // El mismo efecto parallax sutil para consistencia
  background-attachment: fixed;

  // Capa oscura para asegurar la legibilidad del texto
  &::before {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba($MIDA-DARK, 0.75);
    z-index: 1;
  }

  &__container {
    position: relative;
    z-index: 2;
    text-align: center;
    color: $MIDA-LIGHT;
    max-width: 800px;
  }

  &__title {
    font-family: var(--font-poppins);
    font-weight: 800;
    font-size: clamp(2.5rem, 6vw, 4.5rem);
    text-transform: uppercase;
    letter-spacing: 2px;
    margin-bottom: 1rem;
    color: $MIDA-LIGHT;
  }

  &__subtitle {
    font-family: var(--font-poppins);
    font-size: clamp(1rem, 2.5vw, 1.2rem);
    font-weight: 300;
    line-height: 1.7;
    margin-bottom: 2.5rem;
    max-width: 550px;
    margin-left: auto;
    margin-right: auto;
    color: $MIDA-GRAY; // Un color ligeramente diferente para la jerarquía
  }

  &__email {
    font-family: var(--font-poppins);
    font-weight: 500;
    font-size: clamp(1.1rem, 3vw, 1.5rem);
    color: $MIDA-LIGHT;
    text-decoration: none;
    border-bottom: 2px solid transparent;
    transition: color 0.3s ease, border-color 0.3s ease;

    &:hover {
      // Al pasar el mouse, el color cambia a uno de acento y aparece un subrayado
      color: $MIDA-GREEN;
      border-color: $MIDA-GREEN;
    }
  }
}
</style>