<template>
  <v-app dark>
    <v-navigation-drawer
      v-model="drawer"
      :mini-variant="miniVariant"
      fixed
      app
      :floating="true"
    >
      <v-list dense nav>
        <v-list-item v-for="(zone, index) in zones" :key="index" nuxt link>
          <v-list-item-avatar>
            <v-img
              :src="zone.image"
              :alt="'Small avatar images of ' + zone.name"
            ></v-img>
          </v-list-item-avatar>
          <v-list-item-content>
            <nuxt-link
              :to="{
                name: 'zone-id',
                params: {
                  id: zone.name
                }
              }"
            >
              <v-list-item-title class="grey--text subtitle-2">
                {{ zone.name }}
              </v-list-item-title>
            </nuxt-link>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <v-app-bar fixed app>
      <v-app-bar-nav-icon @click.stop="drawer = !drawer"></v-app-bar-nav-icon>
      <nuxt-link :to="{ name: 'index' }" exact>
        <v-toolbar-title class="text-uppercase grey--text">
          <span class="font-weight-light">Wow</span>
          <span>rares</span>
        </v-toolbar-title>
      </nuxt-link>
      <v-toolbar-items>
        <v-btn text disabled class="font-weight-light hidden-sm-and-down">{{
          zone.name
        }}</v-btn>
      </v-toolbar-items>
      <v-spacer />
      <v-btn
        rounded
        light
        class="orange darken-3"
        href="https://www.patreon.com/wowrares"
        target="_blank"
        rel="noreferrer"
      >
        ｡◕‿‿◕｡
      </v-btn>
    </v-app-bar>
    <v-content>
      <v-container>
        <nuxt />
      </v-container>
    </v-content>
    <v-footer :fixed="fixed" inset padless app class="hidden-sm-and-down">
      <v-btn text href="#">
        <span class="font-weight-thin caption">About Wowrares.com</span>
      </v-btn>

      <v-btn text href="#">
        <span class="font-weight-thin caption">Privacy Policy</span>
      </v-btn>

      <v-btn text href="#">
        <span class="font-weight-thin caption">Help</span>
      </v-btn>

      <v-btn text href="#">
        <span class="font-weight-thin caption">Business</span>
      </v-btn>

      <v-btn text href="#">
        <span class="font-weight-thin caption">Advertise</span>
      </v-btn>

      <v-btn text>
        <span class="font-weight-thin caption">Feedback</span>
      </v-btn>

      <v-spacer></v-spacer>

      <v-btn
        icon
        href="https://twitter.com/wowrares_dev"
        target="_blank"
        rel="noreferrer"
      >
        <v-icon color="grey lighten-1">chat</v-icon>
      </v-btn>
    </v-footer>
    <v-btn
      icon
      fab
      href="https://twitter.com/wowrares_dev"
      target="_blank"
      class="hidden-md-and-up"
      rel="noreferrer"
    >
      <v-icon color="grey lighten-1">chat</v-icon>
    </v-btn>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      clipped: false,
      drawer: false,
      fixed: false,
      miniVariant: false,
      title: 'WoWRares'
    }
  },
  computed: {
    zone() {
      return this.$store.state.zone
    },
    zones() {
      return this.$store.state.zones
    }
  }
}
</script>

<style>
.v-application a {
  color: transparent;
}
header {
  background-color: #212121 !important;
}
.theme--dark.v-navigation-drawer {
  background-color: #212121 !important;
}
.v-expansion-panel-header {
  background-color: #212121 !important;
}
.v-expansion-panel-content {
  background-color: #212121 !important;
}
.v-card.v-card--flat.v-sheet.theme--dark {
  background-color: #212121 !important;
}
</style>
