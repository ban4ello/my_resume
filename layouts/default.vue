<template>
  <v-app dark>
    <v-app-bar color="accent" fixed app class="desc_menu">
      <div v-if="!isMobile" class="menu_items">
        <span v-for="(item, i) of menu" :key="i" v-scroll-to="`#${item}`" class="menu_item">
          {{ item }}
        </span>
      </div>

      <v-app-bar-nav-icon v-else @click="drawer = !drawer" />

      <v-spacer />

      <v-app-bar-title>Resume of Ivan Miroshnichenko</v-app-bar-title>

      <div class="ml-4 pointer" @click="swap">
        <v-icon v-if="theme === 'dark'">
          mdi-brightness-6
        </v-icon>
        <v-icon v-else>
          mdi-brightness-4
        </v-icon>
      </div>
    </v-app-bar>

    <v-navigation-drawer
      v-model="drawer"
      temporary
      fixed
      color="accent"
    >
      <v-list nav dense>
        <v-list-item-group v-model="group" class="mobile_menu">
          <v-list-item v-for="(item, i) of menu" :key="i" v-scroll-to="`#${item}`">
            <v-list-item-title>
              <span class="menu_item">{{ item }}</span>
            </v-list-item-title>
          </v-list-item>
        </v-list-item-group>
      </v-list>
    </v-navigation-drawer>

    <v-main>
      <v-container>
        <Nuxt />
      </v-container>
    </v-main>

    <v-footer absolute app color="accent" class="d-flex justify-center">
      <span>&copy; {{ new Date().getFullYear() }}</span>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  name: 'DefaultLayout',

  data () {
    return {
      group: null,
      drawer: false,
      menu: ['summary', 'skills', 'hobby', 'experience', 'contacts']
    }
  },

  computed: {
    theme () {
      return this.$vuetify.theme.isDark ? 'dark' : 'light'
    },
    isMobile () {
      return this.$vuetify.breakpoint.xs || this.$vuetify.breakpoint.sm
    }
  },

  methods: {
    touchAll () {
      const value = this.$vuetify.theme.themes[this.theme]
      this.$vuetify.theme.themes[this.theme] = {}
      this.$vuetify.theme.themes[this.theme] = value
    },

    swap () {
      this.$vuetify.theme.isDark = !this.$vuetify.theme.isDark

      // necessary to reset colors after changing the theme, perhaps a Vuetify.js bug
      this.touchAll(1)
    }
  }
}
</script>
<style lang="scss" scoped>
.desc_menu {
  margin: 0 auto;
  width: 100%;

  .menu_items {
    display: flex;
    gap: 10px;
  }
}

.menu_item {
  text-decoration: none;
  text-transform: capitalize;
}

.mobile_menu .v-list-item__title {
  font-size: 1.2em;
}

.v-application {
  background-color: var(--v-primary-base)
}
</style>
<style lang="scss">
.v-toolbar__content {
  max-width: 1170px;
  margin: 0 auto;
}
</style>
