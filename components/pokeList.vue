<template>
  <div>
    <div v-if="pokeList.length > 380" class="poke-list">
      <div
        v-for="(poke, i) in pokeList"
        :id="`pokemon${i}`"
        :key="i"
        :class="checkKnow(i) ? 'listed-poke show' : 'listed-poke'"
      >
        <img
          :title="checkKnow(i) ? poke.forms[0].name : '???'"
          :src="poke.sprites.front_default"
          :alt="poke.forms[0].name"
          :class="checkKnow(i) ? 'show' : ''"
        />
        <div class="poke-description">
          <img
            src="../assets/icons/has-catch.png"
            alt="catch"
            :title="checkCatched(i) ? 'Has catched!' : 'Dont catched yet'"
            :class="checkCatched(i) ? 'cautch show' : 'cautch'"
          />

          <h4 :class="checkKnow(i) ? 'show' : ''">
            {{ checkKnow(i) ? poke.forms[0].name : '???' }}
          </h4>

          <button
            title="Show dex!"
            :disabled="checkKnow(i) ? false : true"
            :class="checkKnow(i) ? 'show' : ''"
            @click.prevent="viewCurrentDex(i)"
          >
            <img src="../assets/icons/pokedex-icon.png" alt="" />
          </button>
        </div>
      </div>
    </div>

    <internal-pokedex
      :current-name="'internalPokedex'"
      :current-data="pokeList[selectedPoke] ? pokeList[selectedPoke] : {}"
    />
  </div>
</template>

<script lang="ts">
import InternalPokedex from '~/components/InternalPokedex.vue'

export default {
  name: 'PokeList',

  components: {
    InternalPokedex,
  },

  props: {
    pokeList: {
      type: Array,
      default: () => [],
    },
    know: {
      type: Array,
      default: () => [],
    },
    catched: {
      type: Array,
      default: () => [],
    },
    visible: {
      type: Boolean,
      default: false,
    },
  },

  data() {
    return {
      selectedPoke: 0,
    }
  },

  methods: {
    checkKnow(index: number): Boolean {
      return !!(this.know.filter((e) => e === index)[0] !== undefined || null)
    },

    checkCatched(index: number): Boolean {
      return !!(
        this.catched.filter((e) => e === index)[0] !== undefined || null
      )
    },

    viewCurrentDex(index: number): void {
      this.selectedPoke = index
      try {
        document.querySelector('#internalPokedex')!.className = 'main-modal show'
      } catch {}
    },
  },
}
</script>

<style lang="scss">
.selected-poke {
  height: 30vh;
}
.poke-list {
  max-height: 60vh;
  width: 60vh;
  background-color: rgb(100, 100, 100);
  overflow-y: scroll;
  transition: 0.2s;

  border: 20px solid rgb(40, 40, 40);
  border-radius: 10px;

  &:hover {
    width: 90vh;
  }

  .listed-poke {
    display: flex;
    align-items: center;
    justify-content: space-around;
    border-bottom: 2px solid gray;

    &.show {
      background-color: rgb(80, 80, 80);
    }

    img {
      filter: brightness(0);
      transition: filter 0.5s ease-in;

      &.show {
        filter: brightness(1);

        &:hover {
          filter: brightness(1.3);
        }
      }
    }

    img {
      .cautch {
        opacity: 0;
      }
      &.show {
        opacity: 1;
      }
    }

    .poke-description {
      width: 300px;
      display: flex;
      justify-content: space-between;
      align-items: center;

      button {
        background-color: transparent;
        border: none;

        img {
          filter: brightness(0.5);
        }

        &.show {
          transition: 0.3s;
          img {
            filter: brightness(1);
          }
          &:hover {
            transform: rotate(-20deg);
          }
        }
      }
    }

    h4 {
      letter-spacing: 4px;
      font-family: PokemonSolid;
      text-shadow: black 1px -1px, black -1px 1px, black 1px 1px,
        black -1px -1px;
      &.show {
        color: lightgray;
      }
    }
  }
}
</style>
