<template>
  <div class="main-container">
    <nav-bar />
    <nuxt />
  </div>
</template>

<script>
// components
import NavBar from '@/components/NavBar.vue'

export default {
  components: {
    NavBar,
  },
}
</script>

<style lang="scss">
@font-face {
  font-family: PokemonSolid;
  src: url(../assets/pokemon-font/Pokemon-Solid.ttf);
}
@font-face {
  font-family: PokemonHollow;
  src: url(../assets/pokemon-font/Pokemon-Hollow.ttf);
}

*,
*::before,
*::after {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: PokemonSolid;
}
</style>
