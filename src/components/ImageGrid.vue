<!-- src/components/ImageGrid.vue -->
<template>
  <div>
    <SearchBar @search="searchImages" />
    <div>
      <div class="container masonry-bricks-container" v-if="loading">
        <PlaceholderCard v-for="index in 8" :key="index" />
      </div>

      <div v-else-if="!loading && images.length === 0" class="no-images-container">
        <img src="../assets/photos.avif" alt="No images found" />
        <p>Cannot retrieve any image for the search term "{{ searchTerm }}".</p>
      </div>

      <div class="container masonry-bricks-container" v-else>
        <ImageCard
          v-for="(image) in images"
          :key="image.id"
          :image="image"
          @click="openModal(image)"
        />
      </div>
    </div>
    <Modal v-if="selectedImage" :image="selectedImage" @close="closeModal" />
  </div>
</template>

<script>
import axios from 'axios';
import ImageCard from './ImageCard.vue';
import SearchBar from './SearchBar.vue';
import Modal from './ImageModal.vue';
import PlaceholderCard from './PlaceholderCard.vue';

export default {
  components: { ImageCard, SearchBar, Modal, PlaceholderCard },
  data() {
    return {
      images: [],
      selectedImage: null,
      loading: true,
      searchTerm: "",
    };
  },
  mounted() {
    this.searchImages("African");
  },
  methods: {
    async searchImages(query) {
      this.loading = true;
      this.searchTerm = query;
      try {
        const response = await axios.get(
          `https://api.unsplash.com/search/photos`,
          {
            params: { query, per_page: 8 },
            headers: {
              Authorization: `Client-ID ${process.env.VUE_APP_UNSPLASH_ACCESS_KEY}`,
            },
          }
        );
        this.images = response.data.results;
      } catch (error) {
        console.error("Error fetching images:", error);
      } finally {
        this.loading = false;
      }
    },
    openModal(image) {
      this.selectedImage = image;
    },
    closeModal() {
      this.selectedImage = null;
    },
  },
};
</script>

<style lang="scss">
@import "../styles/_variables.scss";

.no-images-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  text-align: center;
  margin-top: 2rem;

  img {
    max-width: 12.5rem;
    margin-bottom: 1rem;
  }

  p {
    font-size: 1.2rem;
    color: $gray-medium;
  }
}

.masonry-bricks-container {
  padding: 0 15rem;
  column-count: 3;
  column-gap: 2rem;
  margin-bottom: 3rem;
  transform: translateY(-4%);
}

.masonry-bricks-container img,
.masonry-bricks-container div {
  width: 100%;
  height: 100%;
  max-width: 100%;
  object-fit: cover;
  break-inside: avoid;
  margin-bottom: 0.5rem;
}

@media only screen and (max-width: 1100px) {
  .masonry-bricks-container {
    column-count: 2;
    transform: translateY(-3%);
    padding: 0 5rem;
  }
}

@media only screen and (max-width: 750px) {
  .masonry-bricks-container {
    column-count: 1;
    transform: translateY(-2%);
    padding: 0 5rem;
  }

  .container {
    max-width: 100%;
    padding: 0 0.5rem;
  }
}
</style>
