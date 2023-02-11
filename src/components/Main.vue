<template>
  <section class="main">

    <img class="logo" :src="logo.url" :alt="logo.tittle">
    <input type="search" v-model="search" class="filter search-bar" placeholder="Ex:pikachu">

    <AppContainer></AppContainer>
  </section>
</template>
<script>
import Container from './Container.vue';

export default {
  components: {
    'AppContainer': Container
  },
  data() {
    return {
      url: 'https://pokeapi.co/api/v2/pokemon/?limit=1279',
      logo: {
        url: 'https://logodownload.org/wp-content/uploads/2017/08/pokemon-logo-4-1.png',
        tittle: 'Logo Pokémon'
      }
    }
  }
}
</script>
<style scoped>
.main {
  align-items: center;
  text-align: center;
  display: block;
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
</style>
