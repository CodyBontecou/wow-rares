<template>
  <v-container grid-list-sm text-xs-center>
    <v-layout row wrap class="pa-3 project">
      <v-flex v-if="zone" xs12 md9>
        <v-img :src="zone.image" :alt="'Map of ' + zone.name">
          <v-layout column fill-height class="lightbox grey--text">
            <v-flex shrink>
              <div v-for="(mob, index) in mobs" :key="index">
                <v-img
                  v-model="mob.active"
                  src="https://classicdb.ch/templates/wowhead/images/map-pin-yellow.png"
                  :alt="'Location of ' + mob.name"
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
              <v-expansion-panel-header class="grey--text">
                {{ mob.name }}
              </v-expansion-panel-header>
              <v-expansion-panel-content v-show="mob.active">
                <v-card flat>
                  <v-layout row wrap class="project">
                    <v-flex xs6 align-self-center>
                      <v-img
                        :src="`${mob.image}`"
                        :alt="'Image of ' + mob.name"
                      ></v-img>
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
      return this.$store.state.zone[0]
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
  async fetch({ store, params }) {
    await store.dispatch('fetchZone', params.id)
    await store.dispatch('fetchMobs', params.id)
  },
  // mounted() {
  //   console.log(this.$route)
  // },
  methods: {
    activateMob(index) {
      this.panel.push(index)
      this.$store.commit('activateMob', index)
    },
    deactivateMob(index) {
      this.panel = []
      this.$store.commit('deactivateMob', index)
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
