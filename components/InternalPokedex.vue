<template>
  <div :id="currentName" class="main-modal">
    <a class="close-modal" @click.prevent="closeModal()">X</a>
    <div class="content-view">
      <!-- <slot></slot> -->
      <h1>{{ currentPokeName() }}</h1>
      <div class="img-content">
        <img @click.prevent="currentImage()" :src="currentImage()" alt="" />
      </div>
    </div>
  </div>
</template>

<script lang="ts">
export default {
  name: 'InternalPokedex',
  props: {
    currentName: {
      type: String,
      default: 'modal',
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
    currentPokeName(): void {
      return this.currentData?.forms ? this.currentData?.forms[0].name : ''
    },
    currentImage(): void {
      return this.currentData?.sprites?.other?.dream_world?.front_default
        ? this.currentData?.sprites?.other?.dream_world?.front_default
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
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    width: 80vw;
    height: 90vh;
    // border: 20px solid lightgray;
    border-radius: 10px;

    background-color: #7b0907;

    h1 {
      margin: 20px;
      text-transform: capitalize;
      color: #ebc908;
      text-shadow: black 2px -2px, black -2px 2px, black 2px 2px,
        black -1px -1px;
      letter-spacing: 4px;
    }
  }
}
</style>
