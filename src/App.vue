<template>
  <div id="app">
    <main class="main-content">
      <ImageGrid />
    </main>
  </div>
</template>

<script>
import ImageGrid from './components/ImageGrid.vue';

export default {
  components: {
    ImageGrid,
  },
};
</script>

<style lang="scss">
@import './styles/variables';

body {
  margin: 0;
  padding: 0;
  font-family: 'Roboto', sans-serif;
}

#app {
  font-family: 'Roboto', sans-serif;
  color: $primary-color;
  text-align: center;
  margin: 0;
  padding: 0;
}

.main-content {
  justify-content: center;
  flex-direction: column;
  align-items: center;
}
</style>
