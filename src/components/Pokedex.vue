<template>
  <v-container>
    <v-row class="text-center">
      <v-col cols="6" class="mx-auto">
        <v-img
          v-if="!pokemon"
          :src="require('../assets/pokeball.png')"
          class="my-3"
          contain
          height="200"
        />
        <div v-if="pokemon">
            <v-row>
                <v-col cols="8">
                <v-img
                :src="pokemon.sprites.other.dream_world.front_default"
                class="my-3"
                contain
                height="200"
                />
                </v-col>
                <v-col cols="4" class="text-left">
                <v-list-item>
                    <v-list-content>
                        <v-list-item-title>{{'Id: ' + pokemon.id}}</v-list-item-title>
                    </v-list-content>
                </v-list-item>
                <v-list-item>
                    <v-list-content>
                        <v-list-item-title>Abilities</v-list-item-title>
                        <v-list-item-subtitle v-for="ability in pokemon.abilities" :key="ability.ability.name">{{ ability.ability.name.toUpperCase() }}</v-list-item-subtitle>
                    </v-list-content>
                </v-list-item>
                <v-list-item>
                    <v-list-content>
                        <v-list-item-title>{{'Height: ' + pokemon.height}}</v-list-item-title>
                    </v-list-content>
                </v-list-item>
                <v-list-item>
                    <v-list-content>
                        <v-list-item-title>{{'Weight: ' + pokemon.weight}}</v-list-item-title>
                    </v-list-content>
                </v-list-item>
                <v-list-item>
                    <v-list-content>
                        <v-list-item-title>{{'Order: ' + pokemon.order}}</v-list-item-title>
                    </v-list-content>
                </v-list-item>
                </v-col>
            </v-row>
        </div>
    <v-form
        @submit.prevent="fetchPokemon"
        lazy-validation
    >
    <v-text-field
      :rules="[rules.required, rules.space]"
      class="my-3"
      label="Pokemon name"
      hide-details="auto"
      v-model="name"
    ></v-text-field>
    <v-btn type="submit">
        <span>Search</span>
    </v-btn>
    <p>
    <span
      v-if="error"
      class="red--text"
    >{{ error + ' no encontrado'}}</span>
    </p>
    </v-form>
    </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  name: 'Pokedex',

  data: () => ({
    name: '',
    pokemon: null,
    error: null,
    rules: {
      required: value => !!value || 'Required.',
      space: value => !!value.trim().length || 'Space strings are not allowed.'
    }
  }),
  methods: {
    fetchPokemon: function () {
      const URI = 'https://pokeapi.co/api/v2/pokemon/' + this.name.trim().toLowerCase()
      this.$http.get(URI)
        .then((result) => {
          this.pokemon = result.data
          this.error = null
        })
        .catch((e) => {
          this.pokemon = null
          this.error = this.name
        })
    }
  }
}
</script>
