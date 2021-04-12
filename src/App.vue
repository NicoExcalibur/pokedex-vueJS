<template>
  <div id="app">
    <Pokemon />
  </div>
</template>

<script>
import Pokemon from '@/components/Pokemon.vue'

export default {
  components: {
    Pokemon
  }
}
</script>

<style>
  
  body {
    margin: 0;
    padding: 0;
    font-family: Arial, Helvetica, sans-serif;
  }

  h1 {
    text-align: center;
  }

</style>
