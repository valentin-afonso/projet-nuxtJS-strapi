<template>
  <div>
    <h2>{{ titre }}</h2>
    <p>Ceci est le component detail house</p>
    <p>{{ prix }} €</p>
    <nuxt-link to="/">Detail</nuxt-link>
  </div>
</template>

<script>
export default {
  name: "TeaserHouse",
  props: ["titre", "prix"],
};
</script>

<style>
</style>