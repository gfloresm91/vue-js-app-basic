<template>
<li class="artista">
  <h2>
    <a :href="artista.url" target="_blank"> {{ artista.name }}</a>
  </h2>
  <img :src="artista.image[2]['#text']">
</li>
</template>

<script>
export default {
  name: 'topartistas',
  props: [ 'artista' ]
}
</script>

<style lang="stylus" scoped>
li.artista
  display block
  margin 10px 0
</style>
