<template>
  <v-app dark>
    <v-app-bar fixed app class="desc_menu">
      <div v-if="!isMobile" class="menu_items">
        <v-toolbar-title v-for="(item, i) of menu" :key="i">
          <a v-scroll-to="`#${item}`" class="menu_item" href="#">{{ item }}</a>
        </v-toolbar-title>
      </div>

      <v-app-bar-nav-icon v-else @click="drawer = !drawer" />

      <v-spacer />

      <v-app-bar-title>Resume of Ivan Miroshnichenko</v-app-bar-title>
    </v-app-bar>

    <v-navigation-drawer
      v-model="drawer"
      temporary
      fixed
      class="mobile_menu"
    >
      <v-list nav dense>
        <v-list-item-group
          v-model="group"
          active-class="deep-purple--text text--accent-4"
        >
          <v-list-item v-for="(item, i) of menu" :key="i" v-scroll-to="`#${item}`">
            <v-list-item-title>
              <a class="menu_item" href="#">{{ item }}</a>
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

    <v-footer absolute app>
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
    isMobile () {
      return this.$vuetify.breakpoint.xs || this.$vuetify.breakpoint.sm
    }
  }
}
</script>
<style lang="scss" scoped>
.desc_menu {
  // max-width: 1170px;
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
  color: #fff;
  // display: flex;
  // grid-gap: 53px;
  // align-items: center;
}
</style>
