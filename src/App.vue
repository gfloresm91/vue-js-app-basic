<template>
  <div id="app">
    <img src="./assets/logo.png">
    <h1>Bienvenido a Vue music con last.fm api</h1>
    <select v-model="selectedCountry">
      <option
        v-for="country in countries"
        :key="country.value"
        :value="country.value"
      >{{ country.name }}</option>
    </select>
    <h2>Top artistas en {{ selectedCountry |capitalize }}</h2>
    <spinner v-show="loading"></spinner>
    <ul>
      <topartistas v-for="artista in artistas" :artista="artista" :key="artista.mbid"></topartistas>
    </ul>
  </div>
</template>

<script>
import topartistas from "./components/topartistas.vue";
import spinner from "./components/spinner.vue";
import getArtists from "./api";

export default {
  name: "app",
  data() {
    return {
      artistas: [],
      countries: [
        { name: "Chile", value: "chile" },
        { name: "Argentina", value: "argentina" },
        { name: "Colombia", value: "colombia" },
        { name: "España", value: "spain" }
      ],
      selectedCountry: "chile",
      loading: true
    };
  },
  components: {
    topartistas,
    spinner
  },
  methods: {
    refreshArtists() {
      const self = this;
      this.loading = true;
      this.artistas = []
      getArtists(this.selectedCountry).then(function(artistas) {
        self.artistas = artistas;
        self.loading = false;
      });
    }
  },
  mounted() {
    this.refreshArtists();
  },
  watch: {
    selectedCountry() {
      this.refreshArtists();
    }
  },
  filters: {
    capitalize: function(str) {
      return str.charAt(0).toUpperCase() + str.slice(1);
    }
  }
};
</script>

<style lang="stylus">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
