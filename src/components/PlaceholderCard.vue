<!-- src/components/PlaceholderCard.vue -->
<template>
    <div class="placeholder-card" :style="{ height: getRandomHeight() }">
      <div class="placeholder-image"></div>
  
      <div class="placeholder-details">
        <div class="placeholder-author"></div>
        <div class="placeholder-location"></div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    methods: {
      getRandomHeight() {
        const heights = ['15.625rem', '18.75rem', '21.875rem', '25rem', '28.125rem'];
        return heights[Math.floor(Math.random() * heights.length)];
      },
    },
  };
  </script>
  
  <style scoped lang="scss">
  @import '@/styles/_variables.scss';
  
  @keyframes shimmer {
    0% {
      background-position: -100% 0;
    }
    100% {
      background-position: 100% 0;
    }
  }
  
  .placeholder-card {
    background-color: $gray-lightest;
    position: relative;
    border-radius: 0.5rem;
    overflow: hidden;
    width: 100%;
  
    .placeholder-image {
      background-color: $gray-lightest;
      display: block;
      width: 100%;
      height: auto;
      border-radius: 0.5rem;
      object-fit: cover;
      animation: shimmer 2s infinite linear;
      background: linear-gradient(
        to right,
        $gray-light 0%,
        $gray-placeholder 20%,
        $gray-light 40%,
        $gray-light 100%
      );
      background-size: 200% 100%;
    }
  
    .placeholder-details {
      padding: 0.3125rem 0.625rem;
      display: flex;
      flex-direction: column;
      justify-content: flex-end;
      position: absolute;
      bottom: 0;
      gap: 0.3125rem;
  
      .placeholder-author,
      .placeholder-location {
        background: linear-gradient(
          to right,
          $gray-placeholder 0%,
          $gray-medium 20%,
          $gray-placeholder 40%,
          $gray-placeholder 100%
        );
        background-size: 200% 100%;
        animation: shimmer 2s infinite linear;
        border-radius: 0.25rem;
      }
  
      .placeholder-author {
        height: 1rem;
        width: 60%;
      }
  
      .placeholder-location {
        height: 0.875rem;
        width: 40%;
      }
    }
  }
  </style>
  