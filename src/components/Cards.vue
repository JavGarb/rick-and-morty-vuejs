<template>
  <div>
    <div>
      <p>Pagina: {{ count }}</p>
      <button @click="decrement">Anterior</button>
      <button @click="increment">Siguiente</button>
    </div>
    <transition name="fade" mode ="out-in">
    <div class="contenedor">
      <div
        v-for="character in characters"
        :key="character.id"
        class="cards"
        
      >
        <img @click="showDetails(character)" :src="character?.image" :alt="character?.name" class="image"/>
        <h3>{{ character?.name }}</h3>
        <p>{{ character?.status }}</p>
        <button @click="changeFavorite(character)">
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

export default {
  name: "Cards",
  data() {
    return {
      characters: [],
      count: 1,
      showModal: false,
      selectedCharacter: {},
      favorites: [],
    };
  },

  methods: {
    changeFavorite(character) {
      character.isFavorite = !character.isFavorite;
      if (character.isFavorite) {
        this.addfavorites(character);
      } else {
        const index = this.favorites.findIndex(
          (char) => char.id === character.id
        );
        if (index !== -1) this.favorites.splice(index, 1);
      }
    },
    addfavorites(character) {
      this.favorites.push(character);
    },
    showDetails(character) {
      this.selectedCharacter = character;
      this.showModal = true;
    },
    increment() {
      this.count++;
      this.getData();
    },
    decrement() {
      if (this.count > 1) {
        this.count--;
        this.getData();
      }
    },
    getData() {
      axios
        .get("https://rickandmortyapi.com/api/character?page=" + this.count)
        .then((response) => {
          this.characters = response.data.results.map((c) => {
            return { ...c, isFavorite: false };
          });
        })
        .catch((error) => console.log(error));
    },
  },

  mounted() {
    this.getData();
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
.cards {
  border: 1px solid black;
  width: max-content;
  margin: 10px;
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

.image:hover{
  box-shadow: 0px 0px 20px blue;
}

.fade-enter-active, .fade-leave-active {
  transition: opacity 0.5s;
}

.fade-enter, .fade-leave-to {
  opacity: 0;
}
</style>
