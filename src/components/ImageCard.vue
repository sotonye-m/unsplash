<!-- src/components/ImageCard.vue -->
<template>
    <div class="card">
      <img :src="image.urls.small" @load="loaded = true" v-show="loaded" />
      <div class="photo-details" v-show="loaded">
        <h5 class="author">{{ image.user.name }}</h5>
        <p class="location">{{ image.user.location || 'Unknown Location' }}</p>
      </div>
      <div class="placeholder" v-if="!loaded"></div>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      image: Object,
    },
    data() {
      return {
        loaded: false,
      };
    },
  };
  </script>
  
  <style lang="scss">
  @import '@/styles/_variables.scss';
  
  .card {
    position: relative;
    border-radius: 0.5rem;
    overflow: hidden;
    width: 100%;
    height: auto;
    cursor: pointer;
  
    img {
      display: block;
      width: 100%;
      height: auto;
      border-radius: 0.5rem;
      object-fit: cover;
    }
  
    .photo-details {
      position: absolute;
      bottom: 0;
      left: 0;
      width: 100%;
      padding: 1rem;
      color: $white;
      z-index: 2;
      display: flex;
      flex-direction: column;
      justify-content: flex-end;
      text-align: left;
      gap: 0.3rem;
  
      .author, .location {
        margin: 0;
      }
  
      .author {
        font-size: 1rem;
        font-weight: 400;
      }
  
      .location {
        font-size: 0.8rem;
        opacity: 0.8;
      }
    }
  
    &::before {
      content: '';
      position: absolute;
      bottom: 0;
      left: 0;
      width: 100%;
      height: 50%;
      background: linear-gradient(to top, rgba($black, 0.6), transparent);
      z-index: 1;
      border-radius: inherit;
      pointer-events: none;
      margin-bottom: inherit;
    }
  
    .placeholder {
      width: 100%;
      background-color: $gray-light;
    }
  }
  </style>  