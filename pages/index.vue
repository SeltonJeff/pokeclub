<template>
  <div class="pokedex-container container">
    <h1 class="title">Your Pokedex</h1>
    <h1 v-if="checkAmount() === false">Loading...</h1>
    <poke-list :poke-list="pokeList" :know="know" :catched="catched" />
  </div>
</template>

<script lang="ts">
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
      know: [
        0, 1, 2, 3, 5, 6, 7, 9, 10, 11, 12, 13, 15, 16, 17, 18, 19, 20, 21, 22,
        23, 24, 25, 26,
      ],
      catched: [2, 5, 6, 7, 12],
    }
  },

  mounted() {
    this.getPokeList()
  },

  methods: {
    API_URL(): string {
      return process.env?.BASE ? process.env.BASE : 'https://pokeapi.co/api/v2'
    },

    async getPokeList(initial: number = 1): Promise<void> {
      const numOfPokes: number = 385

      try {
        for (let i: number = initial; i < numOfPokes; i++) {
          const { data }: never = await axios.get(
            `${this.API_URL()}/pokemon/${i}`
          )
          this.pokeList.push(data)
        }
      } catch {}
    },

    checkAmount(): boolean {
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
  }
}
</style>
