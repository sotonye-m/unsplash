<!-- src/components/SearchBar.vue -->
<template>
  <div class="header">
    <div v-if="showResults" class="search-results-header">
      <i class="fas fa-arrow-left" @click="resetSearch"></i>
      <span>Search Results For <span class="searchTerm">"{{ searchQuery }}"</span></span>
    </div>
    <div v-else class="search-bar">
      <div class="input-wrapper">
        <i class="fas fa-search" @click="search"></i>
        <input
          type="text"
          placeholder="Search for photo"
          v-model="query"
          @keyup.enter="search"
        />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      query: "",
      searchQuery: "",
      showResults: false,
    };
  },
  methods: {
    search() {
      if (this.query) {
        this.searchQuery = this.query;
        this.showResults = true;
        this.$emit("search", this.query); 
      }
    },
    resetSearch() {
      this.query = ""; 
      this.searchQuery = "";
      this.$emit("search", "African");
      this.showResults = false;
    },
  },
};
</script>

<style lang="scss">
@import '@/styles/_variables.scss';

.header {
  background-color: $gray-light;
  color: $primary-color;
  padding: 0rem;
  height: 18.75rem;
  align-content: center;

  .search-bar {
    padding: 1rem;
    text-align: center;
    display:flex;
    justify-content: center;

    .input-wrapper {
      position: relative;
      display: flex;
      width: 80%;

      i {
        position: absolute;
        top: 50%;
        left: 1rem;
        transform: translateY(-50%);
        color: $gray-dark;
        font-size: 1.2rem;
      }

      input {
        padding: 1.5rem;
        padding-left: 3rem; 
        width: 100%;
        border: none;
        border-radius: 8px;
        box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        font-size: 1rem;
      }
    }
  }

  .search-results-header {
    display: flex;
    align-items: center;
    padding: 9rem;
    font-size: 2rem;

    i {
      margin-right: 1rem;
      cursor: pointer;
    }

    span {
      color: $dark-navy;
    }
    .searchTerm{
      color: $slate-blue;
    }
  }
}
@media (max-width: 480px) {
  .header {
    height: 12.5rem;
    .search-bar {
    padding: 1rem;
    text-align: center;

    .input-wrapper {
      position: relative;
      display: inline-block;
      width: 100%;

      i {
        position: absolute;
        top: 50%;
        left: 3rem;
        transform: translateY(-50%);
        color: $gray-dark;
        font-size: 1.2rem;
      }

      input {
        padding: 1.5rem;
        padding-left: 3rem;
        width: unset;
        border: none;
        border-radius: 0.5rem;
        box-shadow: 0 0 0.625rem rgba(0, 0, 0, 0.1);
        font-size: 1rem;
      }
    }
  }
  .search-results-header {
    display: flex;
    align-items: center;
    padding: 2rem;
    font-size: 1rem;
    }
  }
}

@media (max-width: 768px) {
  .header {
    height: 15.625rem;
    .search-bar {
    padding: 1rem;
    text-align: center;
    display:flex;
    justify-content: center;

    .input-wrapper {
      position: relative;
      display: flex;
      width: 80%;

      i {
        position: absolute;
        top: 50%;
        left: 1rem;
        transform: translateY(-50%);
        color: $gray-dark;
        font-size: 1.2rem;
      }

      input {
        padding: 1.5rem;
        padding-left: 3rem;
        width: 100%;
        border: none;
        border-radius: .5rem;
        box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        font-size: 1rem;
      }
    }
  }
  .search-results-header {
    display: flex;
    align-items: center;
    padding: 5rem;
    font-size: 1.3rem;
  }
  }
}
</style>
