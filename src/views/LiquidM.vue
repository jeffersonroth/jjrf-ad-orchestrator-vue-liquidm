<template>
  <v-app
    id="liquidm"
    dark>

    <core-filter />

    <Toolbar />

    <Drawer approute="LiquidM" class="text-align: left !important;" />

    <v-fade-transition mode="out-in">
      <router-view />

      <div v-if="option == 'dashboard'"><Dashboard /></div>
      <div v-else-if="option == 'campaigns'"><Dashboard /></div>
      <div v-else-if="option == 'reports'"><Reports /></div>
    </v-fade-transition>

    <core-footer v-if="$route.name !== 'Maps'" />

  </v-app>
</template>

<script>
//import Menu from '@/components/liquidm/Menu.vue'
import Toolbar from '@/components/liquidm/Toolbar.vue'
import Drawer from '@/components/liquidm/Drawer.vue'
import Dashboard from '@/components/liquidm/Dashboard.vue'
import Campaigns from '@/components/liquidm/Campaigns.vue'
import Reports from '@/components/liquidm/Reports.vue'

const AUTH_TOKEN_LIQUIDM = process.env;

export default {
  name: 'liquidm',
  metaInfo () {
    return {
      title: 'LiquidM'
    }
  },
  data () {
    return {
      query: '',
      results: '',
      error: '',
      loading: false,
      option: '',
    }
  },
  components: {
    Dashboard,
    Campaigns,
    Reports,
    Toolbar,
    Drawer,
  }
}
</script>

<style>
</style>