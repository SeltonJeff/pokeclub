<template>
  <div class="card" style="width: 18rem">
    <h3 class="card-title">{{ title }}</h3>
    <img class="card-img-top" :src="imgSrc" :alt="title" />
    <div class="card-body">
      <p class="card-text">
        {{ description }}
      </p>
      <a :href="internalUrl" class="btn btn-primary">Pokedex</a>
    </div>
  </div>
</template>

<script>
export default {
  name: 'MyCard',
  props: {
    imgSrc: {
      type: String,
      default: '',
    },
    title: {
      type: String,
      default: '',
    },
    description: {
      type: String,
      default: '',
    },
    internalUrl: {
      type: String,
      default: '',
    },
  },
}
</script>

<style lang="scss">
.card {
  display: flex;
  justify-content: center;
  align-items: center;
  .card-title,
  .card-text {
    text-transform: capitalize;
  }
}
</style>
