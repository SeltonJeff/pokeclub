<template>
  <div class="pokedex-container container">
    <h1 class="title">Your Pokedex</h1>
    <h1 v-if="checkAmount() === false" class="loading">
      <img src="../assets/loading.gif" alt="loading" />
      loading...
    </h1>
    <poke-list :poke-list="pokeList" :know="know" :catched="catched" />
  </div>
</template>

<script>
import axios from 'axios'
import Vue from 'vue'

// components
import PokeList from '@/components/pokeList.vue'

export default Vue.extend({
  components: {
    PokeList,
  },

  data() {
    return {
      pokeList: [],
      know: [],
      catched: [],
    }
  },

  mounted() {
    this.getPokeList()
  },

  methods: {
    API_URL() {
      return process.env?.BASE ? process.env.BASE : 'https://pokeapi.co/api/v2'
    },

    async getPokeList(initial = 1) {
      const numOfPokes = 385

      try {
        for (let i = initial; i < numOfPokes; i++) {
          const { data } = await axios.get(`${this.API_URL()}/pokemon/${i}`)
          this.pokeList.push(data)
          this.know.push(i - 1)
        }
      } catch {}
    },

    checkAmount() {
      if (this.pokeList.length > 380) return true
      else return false
    },
  },
})
</script>

<style lang="scss" scoped>
.pokedex-container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 90vh;
  max-width: 70vh;

  background-color: #7b0907;
  box-shadow: 0px 0px 20px black;

  h1 {
    font-weight: lighter;
    color: lightgray;
    text-shadow: black 1px -1px, black -1px 1px, black 1px 1px, black -1px -1px;

    &.title {
      color: rgb(40, 40, 40);
      margin-bottom: 40px;
      text-shadow: white 1px -1px, white -1px 1px, white 1px 1px,
        white -1px -1px;
    }

    &.loading {
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      color: #ebc908;
      text-shadow: black 2px -2px, black -2px 2px, black 2px 2px,
        black -1px -1px;
      img {
        margin-bottom: 50px;
        object-fit: cover;
        max-width: 100px;
      }
    }
  }

  @media (max-width: 700px) {
    height: 90vh;
    max-width: 100vw;

    .title {
      margin: 0;
      font-size: 2em;
    }
  }
}
</style>
