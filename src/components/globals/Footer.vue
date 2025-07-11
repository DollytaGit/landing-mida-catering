<script setup lang="ts">
const currentYear = new Date().getFullYear();
</script>

<template>
  <footer class="footer">
    <div class="footer__container">
      <p class="footer__text">
        &copy; {{ currentYear }} MIDA Catering. Todos los derechos reservados.
      </p>
      <p class="footer__text">
        <span>Diseñado por</span>
        <a href="https://www.instagram.com/yeyo.dev/" target="_blank" rel="noopener noreferrer" title="Visita yeyo.dev">
          yeyodev
        </a>
      </p>
    </div>
  </footer>
</template>

<style lang="scss" scoped>
@use '@/styles/index.scss' as *;

.footer {
  padding: 2.5rem 5%;
  background-color: $MIDA-DARK;

  &__container {
    max-width: 1400px;
    margin: 0 auto;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 1rem;

    // En pantallas más grandes, colocamos los elementos en una fila
    @media(min-width: 768px) {
      flex-direction: row;
      justify-content: space-between;
    }
  }

  &__text {
    font-family: var(--font-poppins);
    font-size: 0.9rem;
    color: $MIDA-GRAY;
    text-align: center;
    margin: 0;

    span {
      margin-right: 0.5rem;
    }
  }

  a {
    color: $MIDA-LIGHT;
    font-weight: 500;
    text-decoration: none;
    position: relative;
    transition: color 0.3s ease;

    // Línea animada para el hover
    &::after {
      content: '';
      position: absolute;
      bottom: -2px;
      left: 0;
      width: 100%;
      height: 1px;
      background-color: $MIDA-GREEN;
      transform: scaleX(0);
      transform-origin: right;
      transition: transform 0.4s ease;
    }

    &:hover {
      color: $MIDA-GREEN;

      &::after {
        transform: scaleX(1);
        transform-origin: left;
      }
    }
  }
}
</style>