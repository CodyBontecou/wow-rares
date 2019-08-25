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
        <v-list-item
          v-for="(zone, index) in zones"
          :key="index"
          nuxt
          link
          @click="mobsInfo(zone)"
        >
          <v-list-item-avatar>
            <v-img :src="zone.image"></v-img>
          </v-list-item-avatar>
          <v-list-item-content>
            <nuxt-link :to="{ name: 'zone-id', params: { id: zone.name } }">
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
        <v-btn text disabled class="font-weight-light hidden-sm-and-down">{{ zone.name }}</v-btn>
      </v-toolbar-items>
      <v-spacer />
      <a
        href="https://www.patreon.com/bePatron?u=20293765"
        data-patreon-widget-type="become-patron-button"
        >Become a Patron!</a
      >
      <script
        async
        src="https://c6.patreon.com/becomePatronButton.bundle.js"
      ></script>
      <!--      <v-btn icon @click.stop="rightDrawer = !rightDrawer">-->
      <!--        <v-icon>mdi-menu</v-icon>-->
      <!--      </v-btn>-->
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

      <v-btn icon href="https://twitter.com/wowrares_dev" target="_blank">
        <v-icon color="grey lighten-1">chat</v-icon>
      </v-btn>
    </v-footer>
    <!--    TODO: Style background to be dark. Move to right side of screen. -->
    <v-btn
      icon
      fab
      href="https://twitter.com/wowrares_dev"
      target="_blank"
      class="hidden-md-and-up"
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
  },
  methods: {
    async mobsInfo(zone) {
      this.$store.commit('setZone', zone)
      await this.$store.dispatch('fetchMobs', zone)
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
</style>
