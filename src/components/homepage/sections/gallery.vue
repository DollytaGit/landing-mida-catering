<script setup lang="ts">

import img1 from '@/assets/gallery/gallery-1.webp';
import img2 from '@/assets/gallery/gallery-2.webp';
import img3 from '@/assets/gallery/gallery-3.webp';
import img4 from '@/assets/gallery/gallery-4.webp';
import img5 from '@/assets/gallery/gallery-5.webp';
import img6 from '@/assets/gallery/gallery-6.webp';
import GalleryCard from '@/components/cards/GalleryCard.vue';

// --- Datos para la Galería ---
const galleryItems = [
  { id: 1, imageSrc: img1, title: 'Bodas de Ensueño', tag: 'Social' },
  { id: 2, imageSrc: img2, title: 'Eventos Nocturnos', tag: 'Catering' },
  { id: 3, imageSrc: img3, title: 'Buffet Ejecutivo', tag: 'Corporativo' },
  { id: 4, imageSrc: img4, title: 'Estaciones de Postres', tag: 'Experiencias' },
  { id: 5, imageSrc: img5, title: 'Menús Programados', tag: 'Delivery' },
  { id: 6, imageSrc: img6, title: 'Cocina de Alta Gama', tag: 'Producción' }
];
</script>

<template>
  <section id="galeria" class="gallery-section">
    <div class="gallery-section__container">
      <h2 class="gallery-section__title">Nuestra Pasión en Imágenes</h2>
      <p class="gallery-section__subtitle">
        Cada plato, cada evento, cada detalle cuenta una historia de sabor y dedicación.
      </p>
      <div class="gallery-section__grid">
        <GalleryCard
          v-for="item in galleryItems"
          :key="item.id"
          :image-src="item.imageSrc"
          :title="item.title"
          :tag="item.tag"
        />
      </div>
    </div>
  </section>
</template>

<style lang="scss" scoped>
@use '@/styles/index.scss' as *;

.gallery-section {
  padding: 6rem 5%;
  background-color: $MIDA-DARK; // Un fondo oscuro para que la galería resalte

  &__container {
    max-width: 1400px;
    margin: 0 auto;
    text-align: center;
  }

  &__title {
    font-family: var(--font-poppins);
    font-weight: 700;
    font-size: clamp(2.2rem, 5vw, 3rem);
    color: $MIDA-LIGHT;
    margin-bottom: 1rem;
  }

  &__subtitle {
    font-family: var(--font-poppins);
    font-size: 1.1rem;
    color: $MIDA-GRAY;
    margin-bottom: 4rem;
    max-width: 600px;
    margin-left: auto;
    margin-right: auto;
  }

  &__grid {
    display: grid;
    // Columnas automáticas que se ajustan, con un mínimo de 300px
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    grid-auto-rows: 250px; // Altura de fila base
    gap: 1.5rem;

    // --- El truco para el layout tipo Masonry ---
    @media (min-width: 768px) {
      grid-template-columns: repeat(4, 1fr); // 4 columnas en desktop

      // Hacemos que ciertos elementos ocupen más espacio
      &> :nth-child(1) {
        grid-column: span 2;
        grid-row: span 2;
      }

      &> :nth-child(4) {
        grid-row: span 2;
      }

      &> :nth-child(5) {
        grid-column: span 2;
      }
    }
  }
}
</style>