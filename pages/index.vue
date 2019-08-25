<template>
  <v-container grid-list-md>
    <v-layout align-top justify-center row wrap class="pa-5">
      <v-flex xs12 sm6 text-xs-center>
        <p
          class="text-uppercase grey--text display-1 font-weight-medium text-center"
        >
          <span class="font-weight-light">Wow</span>
          <span>rares</span>
        </p>
      </v-flex>
    </v-layout>
    <v-layout align-top justify-center row fill-height>
      <v-flex d-flex xs12>
        <p class="grey--text font-weight-medium">
          <span class="">Introducing Wowrares.com</span>
          <span class="font-weight-light"
            >A tool to optimize your WoW Classic experience.</span
          >
        </p>
      </v-flex>
      <v-flex d-flex xs12 md4>
        <v-card color="grey darken-4">
          <v-card-title primary class="title font-weight-light grey--text"
            >Navigate</v-card-title
          >
          <v-img src="nav-cropped.png" alt="Site navigation preview"></v-img>
        </v-card>
      </v-flex>
      <v-flex d-flex xs12 md4>
        <v-card color="grey darken-4">
          <v-card-title primary class="title font-weight-light grey--text"
            >Locate</v-card-title
          >
          <v-img src="timber-only-map.png" alt="Locate rare mobs using these maps"></v-img>
        </v-card>
      </v-flex>
      <v-flex d-flex xs12 md4>
        <v-card color="grey darken-4">
          <v-card-title class="title font-weight-light grey--text"
            >Loot</v-card-title
          >
          <v-img src="timber-3.png" alt="Rare mob Timber being looted"></v-img>
        </v-card>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
export default {
  computed: {
    zones() {
      return this.$store.state.zones
    }
  },
  async fetch({ store }) {
    await store.dispatch('fetchAllZones')
  }
}
</script>
