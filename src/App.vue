<template>
  <section class="main">

    <img class="logo" :src="logo.url" :alt="logo.tittle">
    <input type="search" v-model="search" class="filter search-bar" placeholder="Ex:pikachu">

    {{ clickOnCard }}
    <section class="container">

      <section v-for="pokemon in findPokemon" :key="pokemon.name" v-show="isSearching">

        <section id="card" @click="showCardDetails()">
          <h3 class="card-tittle">{{ pokemon.name }}</h3>
          <img class="card-img"
            :src="`https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${pokemon_id(pokemon)}.png`"
            :alt="pokemon.name">
        </section>

      </section>

    </section>

    <section id="pokemon-details" v-show="toggle">
      <section class="pokemon-data">
        <p>
          {{ selected_pokemon }}

        </p>
        <button @click="closeCardDetails()">X</button>

      </section>
    </section>

  </section>

</template>

<script>
import axios from 'axios'
import './style/global.css'
export default {
  data() {
    return {
      url: 'https://pokeapi.co/api/v2/pokemon/?limit=1279',
      logo: {
        url: 'https://logodownload.org/wp-content/uploads/2017/08/pokemon-logo-4-1.png',
        tittle: 'Logo Pokémon'
      },
      pokemons: [],
      search: "",
      startSearching: false,
      clickOnCard: false,
      toggle: false,
      selected_pokemon: ""
    }
  },

  created() {
    axios.get(this.url)
      .then(response => this.pokemons = response.data, err => console.log(err))

  },

  methods: {

    pokemon_id(pokemon) {
      return pokemon.url.split("/")[6]
    }
    ,
    showCardDetails() {
      this.toggle = true;
      return this.clickOnCard = true;
    },

    closeCardDetails() {
      this.toggle = false;
    }
  },

  mounted() {
    axios.get(this.url).then(response => this.pokemons = response.data.results, err => console.log(err))
  },

  computed: {

    findPokemon() {
      return this.pokemons.filter((item) => {
        return item.name.includes(this.search)
      })
    },

    isSearching() {
      return (this.search != '') ? this.startSearching = true : this.startSearching = false
    },

    showPokemonDetails(id) {
      axios.get(`https://pokeapi.co/api/v2/pokemon/${id}`)
        .then(response =>
          this.selected_pokemon = response.data,
          err => console.log(err))
      console.log(this.selected_pokemon);
    }
  }
}
</script>

<style scoped>
.main {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  position: relative;
  text-align: center;

  justify-items: center;

}

.logo {
  margin-bottom: 2%;
}

.search-bar {
  margin: auto;
  width: 70%;
  height: 50px;
  font-size: 1.8em;
  border-radius: 5px;
  display: block;
  text-indent: 5%;
}

.search-bar::placeholder {
  opacity: 0.5;
}

.container {
  display: inline-flex;
  flex-direction: row;
  flex-wrap: wrap;
  align-content: space-between;
  justify-content: center;
  height: fit-content;
  margin-top: 2%;
  width: 100%;
  gap: 1%;
}

#card {
  display: block;
  background-color: #F3F6F4;
  border: solid 0.1px rgba(0, 0, 0, 0.5);
  border-radius: 10px;
  width: 180px;
  height: 250px;
  margin: 4%;

  -webkit-box-shadow: 3px 3px 1px 0.5px rgba(100, 100, 100, 0.2);
  box-shadow: 3px 3px 1px 0.5px rgba(100, 100, 100, 0.2);
  cursor: pointer;
}

.card-tittle {
  background-color: rgba(30, 50, 50, 0.3);
  color: #444444;
  word-break: keep-all;
  text-transform: capitalize;
  width: 90%;
  margin: 5%;
}

.card-img {
  width: 90%;
}

#card span {
  color: #444444;
}

#pokemon-details {
  display: flex;
  position: absolute;
  align-items: center;
  justify-content: center;
  top: 0;
  width: 100vw;
  height: 100vh;
  background-color: rgba(0, 0, 0, 0.5);
  z-index: 100;

}

.pokemon-data {
  display: flex;
  background-color: #444444;
  border-radius: 10px;
  -webkit-box-shadow: 3px 3px 2px 0.5px rgba(100, 100, 100, 0.5);
  box-shadow: 3px 3px 2px 0.5px rgba(100, 100, 100, 0.5);
  width: 80vw;
  height: 80vh;
  z-index: 1000;
}

.pokemon-data button {
  display: inline;
  justify-items: flex-end;
  font-size: xx-large;
  float: right;

  height: fit-content;
}
</style>
