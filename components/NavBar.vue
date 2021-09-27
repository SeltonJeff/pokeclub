<template>
  <nav class="navbar navbar-expand-lg">
    <a class="navbar-brand title" href="#">PokeClub</a>
    <button
      class="navbar-toggler"
      type="button"
      data-toggle="collapse"
      data-target="#navbarNav"
      aria-controls="navbarNav"
      aria-expanded="false"
      aria-label="Toggle navigation"
    >
      <span class="navbar-toggler-icon"></span>
    </button>
  </nav>
</template>

<script>
export default {
  name: 'NavBar',
}
</script>

<style lang="scss">
.navbar {
  height: 10vh;
  color: white;
  background-color: rgb(40, 40, 40); //#7b0907;
  box-shadow: 0px 0px 10px black;

  a {
    color: lightgray;
    transition: 0.3s;

    &:hover {
      font-family: PokemonHollow;
    }

    &.title {
      font-family: PokemonSolid;
      font-size: 2.5em;
      margin-left: 20px;
      margin-right: 50px;

      color: #ebc908;
      text-shadow: black 2px -2px, black -2px 2px, black 2px 2px,
        black -1px -1px;
      letter-spacing: 4px;
    }
  }
}
</style>
