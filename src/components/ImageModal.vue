<!-- src/components/ImageModal.vue -->
<template>
  <div class="modal" @click.self="close">
    <span class="close-button" @click="close">
      <i class="fas fa-times"></i>
    </span>
    <div class="modal-content">
      <div class="modal-image-container" style="height: max-content;">
        <img :src="image.urls.full" :alt="image.user.name" />
      </div>
      <div class="modal-details">
        <h2>{{ image.user.name }}</h2>
        <p>{{ image.location || 'Unknown Location' }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    image: Object,
  },
  methods: {
    close() {
      this.$emit("close");
    },
  },
};
</script>

<style lang="scss">
@import '@/styles/_variables.scss';

.modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba($black, 0.7); 
  display: flex;
  align-items: center;
  justify-content: center;

  .close-button {
    position: absolute;
    top: 3.125rem;
    right: 6.25rem;
    background: transparent;
    border: none;
    cursor: pointer;
    font-size: 1.5rem;
    color: $gray-medium;
    z-index: 10;
  }

  .modal-content {
    position: relative;
    background: $white;
    border-radius: 0.625rem;
    overflow: hidden;
    max-width: 75rem;
    display: flex;
    flex-direction: column;
    align-items: center;
    margin: 1.25rem;

    .modal-image-container {
      width: 100%;
      max-height: 70vh;
      overflow: hidden;

      img {
        max-width: 100%;
        width: auto;
        height: auto;
        max-height: 70vh;
        object-fit: cover;
      }
    }

    .modal-details {
      width: 100%;
      padding: 1rem;
      text-align: left;
      box-sizing: border-box;

      h2 {
        margin: 0;
        font-size: 1.2rem;
        font-weight: 500;
        color: $dark-slate-blue;
      }

      p {
        margin: 0.5rem 0;
        color: $soft-gray;
      }
    }
  }
}

@media (max-width: 768px) {
  .modal {
    .close-button {
      top: 3.125rem;
      right: 3.125rem;
    }

    .modal-content {
      width: 90%;
      max-height: 90vh;
    }
  }
}
</style>
