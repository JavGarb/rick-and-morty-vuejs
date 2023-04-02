<template>
  <div>
    <div>
      <button @click="showFavoritesModal = true">Ver Favoritos</button>
      <p>Pagina: {{ count }}</p>
      <button @click="decrement">Anterior</button>
      <button @click="increment">Siguiente</button>
      <favorites
        :favorites="favorites"
        v-if="showFavoritesModal"
        :showFavoritesModal="showFavoritesModal"
        @update:showFavoritesModal="showFavoritesModal = $event"
      ></favorites>
    </div>
    <transition name="fade" mode="out-in">
      <div class="contenedor">
        <div v-for="character in characters" :key="character.id" class="cards">
          <img
            @click="showDetails(character)"
            :src="character?.image"
            :alt="character?.name"
            class="image"
          />
          <h3>{{ character?.name }}</h3>
          <p>{{ character?.status }}</p>
          <button
            @click="changeFavorite(character)"
            class="btnFav"
            :class="{ favorite: character.isFavorite }"
          >
            <span v-if="!character.isFavorite">NO Favorite💔</span>
            <span v-else>Favorite 💖</span>
          </button>
        </div>
      </div>
    </transition>
    <div>
      <p>Pagina: {{ contador }}</p>
      <button @click="decrement">Anterior</button>
      <button @click="increment">Siguiente</button>
    </div>
    <div class="modal" v-if="showModal">
      <div class="modal-content">
        <!-- Renderizar información del personaje seleccionado aquí -->
        <div>
          <span v-if="!selectedCharacter.isFavorite">No Favorite 💔</span>
          <span v-else>Favorite 💖</span>
          <button @click="showModal = false">X</button>
        </div>
        <h3>{{ selectedCharacter?.name }}</h3>
        <p>{{ selectedCharacter?.status }}</p>
        <p>{{ selectedCharacter?.species }}</p>
        <p>{{ selectedCharacter?.gender }}</p>
        <img :src="selectedCharacter?.image" :alt="selectedCharacter?.name" />
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Favorites from "./Favorites.vue";

export default {
  name: "Cards",
  components: {
    Favorites,
  },
  data() {
    return {
      characters: [],
      count: 1,
      showModal: false,
      selectedCharacter: {},
      favorites: [],
      showFavoritesModal: false,
    };
  },

  methods: {
    async getCharacters() {
      try {
        const response = await axios.get(`https://rickandmortyapi.com/api/character/?page=${this.count}`);
        this.characters = response.data.results.map((c) => {
          return { ...c, isFavorite: false };
        });
        this.checkFavorites();
      } catch (error) {
        console.error(error);
      }
    },
    increment() {
      this.count++;
      this.getCharacters();
    },
    decrement() {
      if (this.count > 1) {
        this.count--;
        this.getCharacters();
      }
    },
    showDetails(character) {
      this.selectedCharacter = character;
      this.showModal = true;
    },
    changeFavorite(character) {
      character.isFavorite = !character.isFavorite;
      if (character.isFavorite) {
        this.favorites.push(character);
      } else {
        const index = this.favorites.findIndex((c) => c.id === character.id);
        this.favorites.splice(index, 1);
      }
      localStorage.setItem("favorites", JSON.stringify(this.favorites));
    },
    checkFavorites() {
      this.characters.forEach((character) => {
        const index = this.favorites.findIndex((c) => c.id === character.id);
        if (index !== -1) {
          character.isFavorite = true;
        } else {
          character.isFavorite = false;
        }
      });
    },
  },
  mounted() {
    const favorites = JSON.parse(localStorage.getItem("favorites") || "[]");
    this.favorites = favorites.map((c) => {
      return { ...c, isFavorite: true };
    });
    this.getCharacters();
  },
};
</script>

<style scope>
.contenedor {
  width: 100%;
  display: flex;
  flex-wrap: wrap;
  flex-direction: row;
  padding: 10%;
}
.btnFav:hover {
  color: beige;
  background-color: blue;
  transform: scale(1.2);
}
.btnFav {
  color: black;
  background-color: grey;
}
.cards {
  width: max-content;
  margin: 10px;
  color: cyan;
}

.modal {
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

.modal-content {
  background-color: white;
  padding: 20px;
  border-radius: 5px;
  text-align: center;
}

.image:hover {
  box-shadow: 0px 0px 20px blue;
}
.btnFav.favorite {
  box-shadow: 0px 0px 20px yellow;
  background-color: orange;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}

.fade-enter,
.fade-leave-to {
  opacity: 0;
}
</style>
