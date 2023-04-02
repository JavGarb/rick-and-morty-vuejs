<template>
  <div class="favorites-modal" v-if="showFavoritesModal">
    <div class="favorites-modal-content">
      <button @click="closeFavoritesModal" class="close-button">X</button>
      <h2>Personajes Favoritos:</h2>
      <div class="favorites-modal-scroll">
        <p v-if="favorites.length === 0">No hay personajes favoritos</p>
        <div v-else>
          <div
            v-for="favorite in favorites"
            :key="favorite.id"
            class="favorites-card"
          >
            <img :src="favorite.image" :alt="favorite.name" />
            <h3>{{ favorite.name }}</h3>
            <p>{{ favorite.status }}</p>
            <p>{{ favorite.species }}</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Favorites",
  props: {
    favorites: {
      type: Array,
      required: true,
    },
    showFavoritesModal: {
      type: Boolean,
      required: true,
    },
  },
  methods: {
    closeFavoritesModal() {
      this.$emit("update:showFavoritesModal", false);
    },
  },
};
</script>

<style scoped>
.favorites-modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1;
}

.favorites-modal-content {
  position: relative;
  background-image: url(../assets/start.jpeg);
  padding: 20px;
  border-radius: 5px;
  border: 2px solid white;
  text-align: center;
  width: 80%;
  max-height: 80%;
  overflow-y: auto;
}

.favorites-modal-scroll {
  overflow-y: auto;
}

.favorites-card {
  border: 1px solid white;
  background-color: aquamarine;
  width: max-content;
  margin: 10px;
  padding: 10px;
  display: inline-block;
}

.close-button {
  position: absolute;
  top: 20px;
  right: 20px;
  background-color: red;
  color: green;
  border-radius: 50%;
  padding: 10px;
  box-shadow: 0px 0px 10px green;
}

.close-button:hover {
  animation: glow 1s infinite;
}

@keyframes glow {
  0% {
    box-shadow: 0px 0px 10px white;
    background-color: red;
  }
  50% {
    box-shadow: 0px 0px 50px white;
    background-color: green;
  }
  100% {
    box-shadow: 0px 0px 10px white;
    background-color: red;
  }
}

@media (max-width: 768px) {
  .favorites-modal-content {
    width: 90%;
  }
}
</style>
