<template>
  <v-app
    id="liquidm"
    dark>

    <core-filter />

      <core-toolbar />

      <Drawer approute="LiquidM" />

      <v-fade-transition mode="out-in">
        <router-view />
      </v-fade-transition>

      <div v-if="option == 'dashboard'"><Dashboard/></div>

      <core-footer v-if="$route.name !== 'Maps'" />

  </v-app>
</template>

<script>
//import Menu from '@/components/liquidm/Menu.vue'
import Dashboard from '@/components/liquidm/Dashboard.vue'
import Drawer from '@/components/liquidm/Drawer.vue'
export default {
  name: 'liquidm',
  data () {
    return {
      username: '',
      results: '',
      error: '',
      loading: false,
      option: 'dashboard',
    }
  },
  components: {
    Dashboard,
    Drawer,
  }
}
</script>

<style>
</style>