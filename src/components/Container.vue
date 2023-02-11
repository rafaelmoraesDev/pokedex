<template>
  <section class="container">

    <section v-for="pokemon in findPokemon" :key="pokemon.name" v-show="isSearching">

      <section id="card" v-on:click="showCard(pokemon.name)">
        <h3 class="card-tittle">{{ pokemon.name }}</h3>
        <img class="card-img"
          :src="`https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${pokemon_id(pokemon)}.png`"
          :alt="pokemon.name">
      </section>

    </section>

  </section>

</template>
<script>
export default {
  data() {
    return {
      pokemons: [],
      search: "",
      startSearching: false,
      card: {
        name: '',
        evolutions: ''
      }
    }
  },created() {
    this.$http.get(this.url)
      .then(response => this.pokemons = response.data)

  }, methods: {
    pokemon_id(pokemon) {
      return pokemon.url.split("/")[6]
    },
    findPokemon(url) {
      if (this.search !== '') {
        this.$emit
      }
    }, showCard(name) {
      alert(name);
    }
  }, mounted() {
    axios.get(this.url).then(response => this.pokemons = response.data.results, err => console.log(err))
  }, computed: {
    findPokemon() {
      return this.pokemons.filter((item) => {
        return item.name.includes(this.search)
      })
    },
    isSearching() {
      return (this.search != '') ? this.startSearching = true : this.startSearching = false
    }
  }
}
</script>
<style scoped>
.container {
  height: fit-content;
  margin-top: 2%;
  width: 100%;
  display: inline-flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: center;
  gap: 1%;
  align-content: space-between;
}

#card {
  display: block;
  background-color: #F3F6F4;
  border: solid 0.1px rgba(100, 100, 100, 0.5);

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
  width: 90%;
  margin: 5%;

  word-break: keep-all;
  text-transform: capitalize;
  color: #444444;
}

.card-img {
  width: 90%;
}
</style>
