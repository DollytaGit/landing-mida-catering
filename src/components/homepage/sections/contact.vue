<script setup lang="ts">
import { ref } from 'vue';
import contactBgImage from '@/assets/contact/contact-img.webp';

// --- CONSTANTES ---
const emailAddress = 'contacto@mida.com.ec';

// --- ESTADO REACTIVO ---
// 'displayText' controla el texto que se muestra en el botón.
const displayText = ref(emailAddress);
// 'isCopied' nos ayuda a cambiar el estilo del botón como feedback.
const isCopied = ref(false);

// --- LÓGICA DEL COMPONENTE ---
const copyEmailToClipboard = async () => {
  // Prevenimos múltiples clicks si ya está en estado "Copiado".
  if (isCopied.value) return;

  try {
    // Usamos la API del Portapapeles para copiar el texto.
    await navigator.clipboard.writeText(emailAddress);

    // Si la copia es exitosa, actualizamos el estado para dar feedback.
    isCopied.value = true;
    displayText.value = '¡Correo Copiado!';

    // Después de 2.5 segundos, revertimos el estado al original.
    setTimeout(() => {
      displayText.value = emailAddress;
      isCopied.value = false;
    }, 2500);

  } catch (err) {
    console.error('Error al intentar copiar el correo: ', err);
    // Opcional: podrías mostrar un mensaje de error al usuario.
    displayText.value = 'Error al copiar';
    setTimeout(() => {
      displayText.value = emailAddress;
    }, 2500);
  }
};
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

      <button
        type="button"
        class="contact-section__email-btn"
        @click="copyEmailToClipboard"
        :class="{ 'copied': isCopied }"
        aria-label="Copiar correo al portapapeles"
      >
        {{ displayText }}
      </button>

    </div>
  </section>
</template>

<style lang="scss" scoped>
@use '@/styles/index.scss' as *;

.contact-section {
  position: relative;
  padding: 6rem 5%;
  min-height: 60vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  background-size: cover;
  background-position: center;
  background-attachment: fixed;

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
    color: $MIDA-GRAY;
  }

  // --- Estilos para el nuevo botón de copiar ---
  &__email-btn {
    // Reseteamos los estilos por defecto de un botón
    background: none;
    border: none;
    padding: 0;
    font: inherit;
    cursor: pointer;
    outline: inherit;
    font-family: var(--font-poppins);
    font-weight: 500;
    font-size: clamp(1.1rem, 3vw, 1.5rem);
    color: $MIDA-LIGHT;
    text-decoration: none;
    border-bottom: 2px solid transparent;
    padding-bottom: 4px; // Pequeño ajuste para que el borde no esté tan pegado
    transition: color 0.3s ease, border-color 0.3s ease;

    &:hover:not(.copied) {
      // Efecto hover solo cuando no está en estado "copiado"
      color: $MIDA-GREEN;
      border-color: $MIDA-GREEN;
    }

    // Estilo para el estado de feedback "¡Copiado!"
    &.copied {
      color: $MIDA-GREEN;
      border-color: $MIDA-GREEN;
      cursor: default;
    }
  }
}
</style>