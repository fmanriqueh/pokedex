<template>
  <v-app>
    <v-app-bar app>
      <div class="d-flex align-center">
        <v-img
          alt="Vuetify Logo"
          class="shrink mr-2"
          contain
          src="https://cdn.vuetifyjs.com/images/logos/vuetify-logo-dark.png"
          transition="scale-transition"
          width="40"
        />
      </div>
      <v-toolbar-title class="text-uppercase">Pokedex</v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn icon>
        <v-img
          :src="require('./assets/git-hub-64.png')"
          height="50"
          width="50"
        />
      </v-btn>
    </v-app-bar>
    <v-main>
      <Pokedex/>
    </v-main>
  </v-app>
</template>

<script>
// import HelloWorld from './components/HelloWorld'
import Pokedex from './components/Pokedex'

export default {
  name: 'App',

  components: {
    Pokedex
  },

  data: () => ({
  })
}
</script>
