<script setup lang="ts">
defineProps({
  imageSrc: {
    type: String,
    required: true,
  },
  title: {
    type: String,
    required: true,
  },
  tag: {
    type: String,
    required: true,
  },
});
</script>

<template>
  <article class="gallery-card" :style="{ backgroundImage: `url(${imageSrc})` }">
    <div class="gallery-card__overlay">
      <span class="gallery-card__tag">{{ tag }}</span>
      <h3 class="gallery-card__title">{{ title }}</h3>
    </div>
  </article>
</template>

<style lang="scss" scoped>
@use '@/styles/index.scss' as *;

.gallery-card {
  position: relative;
  overflow: hidden;
  border-radius: 8px;
  background-size: cover;
  background-position: center;
  box-shadow: 0 4px 15px rgba($MIDA-DARK, 0.1);

  // Transición suave para el efecto de la imagen de fondo
  transition: transform 0.4s ease, box-shadow 0.4s ease, background-position 0.8s ease;

  // Un sutil efecto de zoom en la imagen al hacer hover
  &:hover {
    box-shadow: 0 12px 35px rgba($MIDA-DARK, 0.2);
    transform: scale(1.03); // Ligero crecimiento de la tarjeta

    .gallery-card__overlay {
      opacity: 1;
      transform: translateY(0);
      backdrop-filter: blur(2px); // Desenfoque sutil del fondo
    }
  }

  &__overlay {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;

    display: flex;
    flex-direction: column;
    justify-content: flex-end; // Alineamos contenido abajo
    align-items: flex-start;
    padding: 1.5rem;

    background: linear-gradient(to top, rgba($MIDA-GREEN, 0.85), rgba($MIDA-GREEN, 0.1));
    color: $MIDA-LIGHT;

    // Estado inicial de la capa de información
    opacity: 0;
    transform: translateY(20px); // Empieza ligeramente abajo
    transition: opacity 0.4s ease, transform 0.4s ease, backdrop-filter 0.4s ease;
  }

  &__tag {
    position: absolute;
    top: 1.5rem;
    right: 4rem;
    font-family: var(--font-poppins);
    font-weight: 600;
    font-size: 0.8rem;
    padding: 0.25rem 0.75rem;
    background-color: rgba($MIDA-DARK, 0.4);
    border-radius: 4px;
    text-transform: uppercase;
  }

  &__title {
    font-family: var(--font-poppins);
    font-size: 1.75rem;
    font-weight: 700;
    line-height: 1.2;
    text-shadow: 0 2px 5px rgba($MIDA-DARK, 0.5);
  }
}
</style>