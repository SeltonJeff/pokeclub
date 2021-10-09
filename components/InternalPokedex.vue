<template>
  <div :id="currentName" class="main-modal">
    <a class="close-modal" @click.prevent="closeModal()">X</a>
    <div class="content-view">
      <div class="principal">
        <!-- pokeimage -->
        <div class="img-content">
          <!-- pokename -->
          <h1>{{ currentData.name !== undefined ? currentData.name : '' }}</h1>
          <img :src="currentImage()" alt="" @click.prevent="" />
        </div>

        <!-- types -->
        <h3 v-for="(type, i) in currentData.types" :key="i">
          Tipo: <span :class="type.type.name"> {{ getType(i) }} </span>
        </h3>
      </div>

      <!-- stats -->
      <div class="stats">
        <h2>Stats</h2>
        <div class="stats__stat">
          Vitalidade:
          <span>
            {{
              currentData.stats !== undefined
                ? currentData.stats[0].base_stat
                : ''
            }}
          </span>
        </div>
        <div class="stats__stat">
          Ataque:
          <span>
            {{
              currentData.stats !== undefined
                ? currentData.stats[1].base_stat
                : ''
            }}
          </span>
        </div>
        <div class="stats__stat">
          Defesa:
          <span>
            {{
              currentData.stats !== undefined
                ? currentData.stats[2].base_stat
                : ''
            }}
          </span>
        </div>
        <div class="stats__stat">
          Velocidade:
          <span>
            {{
              currentData.stats !== undefined
                ? currentData.stats[5].base_stat
                : ''
            }}
          </span>
        </div>
        <div class="stats__stat">
          Peso:
          <span>
            {{ currentData.weight !== undefined ? currentData.weight : '' }}
          </span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'InternalPokedex',
  props: {
    currentName: {
      type: String,
      default: '',
    },
    currentData: {
      type: Object,
      default: () => {},
    },
  },

  data() {
    return {
      isShiny: false,
    }
  },

  methods: {
    closeModal() {
      document.querySelector(`#${this.currentName}`).className = 'main-modal'
    },
    currentImage() {
      return this.currentData.sprites?.other?.dream_world?.front_default
        ? this.currentData.sprites.other.dream_world?.front_default
        : ''
    },
    getType(num) {
      return this.currentData.types !== undefined
        ? this.currentData.types[num].type.name
        : ''
    },
  },
}
</script>

<style lang="scss">
.main-modal {
  display: none;
  z-index: 100;
  position: absolute;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background-color: rgba(0, 0, 0, 0.7);
  backdrop-filter: blur(4px) saturate(150%);

  &.show {
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .close-modal {
    position: absolute;
    top: 0;
    left: calc(100vw - 50px);
    height: 50px;
    width: 50px;
    display: flex;
    justify-content: center;
    align-items: center;
    cursor: pointer;
    transition: 0.2s;
    color: lightgray;
    font-size: 1.2em;

    &:hover {
      color: white;
      font-size: 2em;
    }
  }
  .content-view {
    position: relative;
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    width: 80%;
    height: 90%;
    border-radius: 10px;

    background-color: #7b0907;

    text-transform: capitalize;
    color: #fffae0;
    text-shadow: black 2px -2px, black -2px 2px, black 2px 2px, black -1px -1px;
    letter-spacing: 4px;

    .principal {
      display: flex;
      flex-direction: column;
      align-items: center;
    }

    .stats {
      text-align: center;

      span {
        color: #ebc908;
      }
    }

    h1,
    h2 {
      color: #ebc908;
    }
    h2 {
      margin: 20px;
    }

    .img-content {
      margin: 0 20px 20px 20px;
      text-align: center;
      img {
        max-width: 90%;
        max-height: 50vw;
      }
    }

    .fire {
      color: #fc0000;
    }
    .water {
      color: #0026ff;
    }
    .grass {
      color: #66af06;
    }
    .electric {
      color: #ffee00;
    }
    .fighting {
      color: #857c00;
    }
    .ice {
      color: #94fff6;
    }
    .psychic {
      color: #0a5700;
    }
    .bug {
      color: #6e9169;
    }
    .poison {
      color: #55297e;
    }
    .normal {
      color: #472e0d;
    }
    .dark {
      color: #2b2b2b;
    }
    .ground {
      color: #af6f3a;
    }
    .iron,
    .steel {
      color: #b8b8b8;
    }
    .rock {
      color: #5a5a5a;
    }
    .flying {
      color: #00f7ff;
    }
    .ghost {
      color: #363442;
    }
    .dragon {
      color: #ce6b0f;
    }
    .fairy {
      color: #df86af;
    }
  }

  @media (max-width: 600px) {
    .content-view {
      flex-direction: column;
    }
  }
}
</style>
