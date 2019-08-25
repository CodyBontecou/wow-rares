<template>
  <v-container grid-list-sm text-xs-center>
    <v-layout row wrap class="pa-3 project">
      <v-flex v-if="zone" xs12 md9>
        <v-img :src="zone.image" :alt="'Map of ' + zone.name">
          <!--          <div v-show="map_stats">-->
          <!--            {{ active_mob.name }}<br />{{ active_mob.level }}<br />{{-->
          <!--              active_mob.health-->
          <!--            }}-->
          <!--          </div>-->
          <v-layout column fill-height class="lightbox white--text">
            <v-flex shrink>
              <div v-for="(mob, index) in mobs" :key="index">
<!--                TODO: Dynamically load image name into alt tag -->
                <v-img
                  v-model="mob.active"
                  src="https://classicdb.ch/templates/wowhead/images/map-pin-yellow.png"
                  alt="Image of mob"
                  height="11px"
                  width="11px"
                  :style="{
                    top: mob.y_coordinate + '%',
                    left: mob.x_coordinate + '%',
                    position: 'absolute'
                  }"
                  @click="activateMob(index)"
                  @mouseover="changeCursorToPoint()"
                  @mouseleave="changeCursorToDefault()"
                >
                </v-img>
              </div>
            </v-flex>
          </v-layout>
        </v-img>
      </v-flex>
      <v-flex xs12 md3>
        <v-container>
          <v-expansion-panels v-model="panel" multiple>
            <v-expansion-panel v-for="(mob, index) in mobs" :key="index" expand>
              <v-expansion-panel-header>
                {{ mob.name }}
              </v-expansion-panel-header>
              <v-expansion-panel-content v-show="mob.active">
                <v-card flat>
                  <v-layout row wrap class="project">
                    <v-flex xs6 align-self-center>
                      <v-img :src="`${mob.image}`" alt=""></v-img>
                    </v-flex>
                    <v-flex xs6>
                      <v-flex align-self-center>
                        <div class="caption grey--text">Damage</div>
                        <div>{{ mob.damage }}</div>
                      </v-flex>
                      <v-flex align-self-center>
                        <div class="caption grey--text">Health</div>
                        <div>{{ mob.health }}</div>
                      </v-flex>
                      <v-flex align-self-center>
                        <div class="caption grey--text">Level</div>
                        <div>{{ mob.level }}</div>
                      </v-flex>
                    </v-flex>
                  </v-layout>
                </v-card>
              </v-expansion-panel-content>
            </v-expansion-panel>
          </v-expansion-panels>
        </v-container>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      dataReady: false,
      show: false,
      panel: []
    }
  },
  computed: {
    map_stats() {
      return this.$store.state.active
    },
    zone() {
      return this.$store.state.zone
    },
    zones() {
      return this.$store.state.zones
    },
    active_mob() {
      return this.$store.state.active_mob
    },
    mobs() {
      return this.$store.state.mobs
    },
    items() {
      return this.$store.state.items
    }
  },
  async fetch({ store }) {
    await store.dispatch('fetchAllZones')
  },
  mounted() {
    const fullPath = this.$route.fullPath
    const zone = fullPath.substring(fullPath.lastIndexOf('/') + 1)
    // this.mobsInfo(zone)
    // this.dataReady = true
  },
  methods: {
    async mobsInfo(zone) {
      this.$store.commit('setZone', zone)
      await this.$store.dispatch('fetchMobs', zone)
    },
    mouseOver(mob) {
      this.$store.commit('activateMob', mob)
      this.$store.commit('changeActive')
    },
    mouseOff(mob) {
      this.$store.commit('activateMob', mob)
      this.$store.commit('changeActive')
    },
    activateMob(index) {
      this.panel.push(index)
      this.$store.commit('activateMob', index)
    },
    deactivateMob(index) {
      this.panel = []
      this.$store.commit('deactivateMob', index)
    },
    hoverItem(item) {
      console.log(item.name)
    },
    changeCursorToPoint() {
      document.body.style.cursor = 'pointer'
    },
    changeCursorToDefault() {
      document.body.style.cursor = 'default'
    }
  }
}
</script>
