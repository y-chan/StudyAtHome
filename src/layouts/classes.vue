<template>
  <v-app>
    <v-overlay v-if="loading" color="#F8F9FA" opacity="1" z-index="9999">
      <div class="loader">
        Loading
      </div>
    </v-overlay>
    <!--
    <v-navigation-drawer
      v-model="drawer"
      :mini-variant="miniVariant"
      :clipped="clipped"
      fixed
      app
    >
      <v-list>
        <v-list-item
          v-for="(item, i) in items"
          :key="i"
          :to="item.to"
          router
          exact
        >
          <v-list-item-action>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title v-text="item.title" />
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    -->
    <v-app-bar
      fixed
      app
      dense
      style="
        background-color: rgba(0, 0, 0, 0);
        color: white;
        text-align: center;
      "
      elevation="0"
    >
      <span>
        {{ schoolName }}
      </span>
      <v-spacer />
      <div class="date">
        <v-btn icon small dark @click="prevDate">
          <v-icon>mdi-chevron-left</v-icon>
        </v-btn>
        <v-btn text dark style="padding: 0 0;">
          {{ ViewDate }}
        </v-btn>
        <v-btn icon small dark @click="nextDate">
          <v-icon>mdi-chevron-right</v-icon>
        </v-btn>
      </div>
      <span>
        {{ className }}
      </span>
    </v-app-bar>
    <v-content style="background-color: #0071c2;">
      <v-container class="px-4 py-8">
        <nuxt />
      </v-container>
    </v-content>
    <v-footer dark color="#0071c2">
      <span>&copy; Code For Japan {{ new Date().getFullYear() }}</span>
    </v-footer>
  </v-app>
</template>

<script>
import { mapGetters, mapActions } from 'vuex'
export default {
  middleware: 'checkClassData',
  computed: {
    ...mapGetters('modules/class', ['schoolName', 'className', 'ViewDate']),
  },
  data() {
    return {
      loading: true,
    }
  },
  mounted() {
    this.loading = false
    this.setViewDate(this.$dayjs().format('YYYY-MM-DD'))
  },
  methods: {
    ...mapActions('modules/class', ['setViewDate', 'prevDate', 'nextDate']),
  },
}
</script>

<style scoped>
.date-icon {
  margin-right: 15px;
}
.date {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
</style>
