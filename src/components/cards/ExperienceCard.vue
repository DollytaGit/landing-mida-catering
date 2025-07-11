<script setup lang="ts">
// Definimos las props que el componente espera recibir del padre.
// Esta es la forma idiomática y robusta de declarar props en Vue 3 con TypeScript.
defineProps({
  imageSrc: {
    type: String,
    required: true,
  },
  title: {
    type: String,
    required: true,
  },
  description: {
    type: String,
    required: true,
  },
});
</script>

<template>
  <article class="card">
    <div class="card__image-container">
      <img :src="imageSrc" :alt="`Imagen de servicio ${title}`" class="card__image" loading="lazy" />
    </div>
    <div class="card__content">
      <h3 class="card__title">{{ title }}</h3>
      <p class="card__description">{{ description }}</p>
    </div>
  </article>
</template>

<style lang="scss" scoped>
@use '@/styles/index.scss' as *;

.card {
  background-color: $MIDA-LIGHT;
  border-radius: 8px;
  overflow: hidden;
  display: flex;
  flex-direction: column;
  // Sombra sutil y profesional
  box-shadow: 0 4px 25px rgba($MIDA-DARK, 0.08);
  transition: transform 0.3s ease, box-shadow 0.3s ease;

  // El efecto hover que eleva la percepción de calidad
  &:hover {
    transform: translateY(-8px);
    box-shadow: 0 12px 35px rgba($MIDA-DARK, 0.12);
  }

  &__image-container {
    width: 100%;
    // Forzamos una proporción para que todas las imágenes luzcan uniformes
    aspect-ratio: 16 / 10;
  }

  &__image {
    width: 100%;
    height: 100%;
    object-fit: cover; // Asegura que la imagen cubra el contenedor sin deformarse
  }

  &__content {
    padding: 1.5rem;
    flex-grow: 1;
    display: flex;
    flex-direction: column;
  }

  &__title {
    font-family: var(--font-poppins);
    font-size: 1.5rem;
    font-weight: 600;
    color: $MIDA-DARK;
    margin-bottom: 0.75rem;
  }

  &__description {
    font-family: var(--font-poppins);
    font-size: 0.95rem;
    line-height: 1.6;
    color: $MIDA-COFFEE;
    flex-grow: 1; // Asegura que el párrafo ocupe el espacio disponible
  }
}
</style>