<script setup lang="ts">
import socialImg from '@/assets/experience/experience-1.webp';
import corporativoImg from '@/assets/experience/experience-2.webp';
import asesoriasImg from '@/assets/experience/experience-3.webp';
import ExperienceCard from '@/components/cards/ExperienceCard.vue';

const experiences = [
  {
    id: 'social',
    imageSrc: socialImg,
    title: 'Social',
    description: 'Menús que complementan tus eventos sociales: Bodas, bautizos, cumpleaños, fiestas temáticas y mucho más.'
  },
  {
    id: 'corporativo',
    imageSrc: corporativoImg,
    title: 'Corporativo',
    description: 'Te acompañamos a ti y a tus colaboradores en eventos, almuerzos empresariales, coffe breaks y deliverys.'
  },
  {
    id: 'asesorias',
    imageSrc: asesoriasImg,
    title: 'Asesorías',
    description: 'Nuestro equipo de profesionales te asistirá en master class, renovación de carta, ferias y otras soluciones gastronómicas.'
  }
];
</script>

<template>
  <section id="experiencias" class="experiences-section">
    <div class="experiences-section__container">
      <h2 class="experiences-section__title">Experiencias culinarias</h2>
      <p class="experiences-section__subtitle">
        Permite que MIDA Catering eleve tus celebraciones a un nivel superior
      </p>
      <div class="experiences-section__grid">
        <ExperienceCard
          v-for="exp in experiences"
          :key="exp.id"
          :image-src="exp.imageSrc"
          :title="exp.title"
          :description="exp.description"
        />
      </div>
    </div>
  </section>
</template>

<style lang="scss" scoped>
@use '@/styles/index.scss' as *;

.experiences-section {
  padding: 6rem 5%;
  background-color: $text-light;

  &__container {
    max-width: 1200px;
    margin: 0 auto;
    text-align: center;
  }

  &__title {
    font-family: var(--font-poppins);
    font-weight: 700;
    font-size: clamp(2.2rem, 5vw, 3rem);
    color: $MIDA-DARK;
    margin-bottom: 1rem;
  }

  &__subtitle {
    font-family: var(--font-poppins);
    font-size: 1.1rem;
    color: $MIDA-COFFEE;
    margin-bottom: 4rem; // Espacio generoso antes de las tarjetas
    max-width: 500px;
    margin-left: auto;
    margin-right: auto;
  }

  &__grid {
    display: grid;
    // En móvil, una columna. En desktop, tres.
    grid-template-columns: 1fr;
    gap: 2rem; // Espacio entre tarjetas

    // Media query para tablets y desktop
    @media (min-width: 768px) {
      grid-template-columns: repeat(3, 1fr);
      gap: 2.5rem;
    }
  }
}
</style>