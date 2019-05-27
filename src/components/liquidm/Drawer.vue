<template>
  <v-navigation-drawer
    id="liquidm-drawer"
    v-model="inputValue"
    app
    dark
    floating
    persistent
    mobile-break-point="991"
    width="260"
  >
    <v-img
      :src="image"
      height="100%"
    >
      <v-layout
        class="fill-height"
        tag="v-list"
        column
      >
        <v-list-tile avatar>
          <v-list-tile-avatar
            color="grey"
          >
            <v-img
              :src="logo"
              height="40"
              contain
            />
          </v-list-tile-avatar>
          <v-list-tile-title class="title">
            {{ approute }}
          </v-list-tile-title>
        </v-list-tile>
        <v-divider/>
        <v-list-tile
          v-if="responsive"
        >
          <v-text-field
            class="purple-input search-input"
            label="Search..."
            color="purple"
          />
        </v-list-tile>
        <v-list-tile
          v-for="(link, i) in links"
          :key="i"
          :to="link.to"
          :active-class="color"
          avatar
          class="v-list-item"
        >
          <v-list-tile-action>
            <v-icon>{{ link.icon }}</v-icon>
          </v-list-tile-action>
          <v-list-tile-title
            v-text="link.text"
          />
        </v-list-tile>
      </v-layout>
    </v-img>
  </v-navigation-drawer>
</template>

<script>
// Utilities
import {
  mapMutations,
  mapState
} from 'vuex'

export default {
  name: "Drawer",
  props: {
    approute: String
  },
  data: () => ({
    logo: require('@/assets/img/logo.png'),
    links: [
      {
        to: '/liquidm/dashboard',
        icon: 'mdi-view-dashboard',
        text: 'Dashboard'
      },
      {
        to: '/liquidm/campaigns',
        icon: 'mdi-table-edit',
        text: 'Campaigns'
      },
      {
        to: '/liquidm/reports',
        icon: 'mdi-clipboard-outline',
        text: 'Reports'
      },
      {
        to: '/liquidm/stats',
        icon: 'mdi-chart-bubble',
        text: 'Data Analysis'
      },
      {
        to: '/liquidm/geo',
        icon: 'mdi-map-marker',
        text: 'Geo'
      },
      {
        to: '/liquidm/accounts',
        icon: 'mdi-account',
        text: 'Accounts'
      },
      {
        to: '/liquidm/templates',
        icon: 'mdi-format-font',
        text: 'Templates'
      },
      {
        to: '/liquidm/notifications',
        icon: 'mdi-bell',
        text: 'Notifications'
      },
    ],
    responsive: false
  }),
  computed: {
    ...mapState('app', ['image', 'color']),
        inputValue: {
      get () {
        return this.$store.state.app.drawer
      },
      set (val) {
        this.setDrawer(val)
      }
    },
    items () {
      return this.$t('Layout.View.items')
    }
  },
  mounted () {
    this.onResponsiveInverted()
    window.addEventListener('resize', this.onResponsiveInverted)
  },
  beforeDestroy () {
    window.removeEventListener('resize', this.onResponsiveInverted)
  },
  methods: {
    ...mapMutations('app', ['setDrawer', 'toggleDrawer']),
    onResponsiveInverted () {
      if (window.innerWidth < 991) {
        this.responsive = true
      } else {
        this.responsive = false
      }
    }
  }
}
</script>

<style lang="scss">
  #liquidm-drawer {
    .v-list__tile {
      border-radius: 4px;
      align-items: left !important;
      align-self: left !important;
      text-align: left !important;
      margin-left: 0px !important;

      &--buy {
        margin-top: auto;
        margin-bottom: 17px;
      }
    }

    .v-image__image--contain {
      top: 9px;
      height: 60%;
    }

    .search-input {
      margin-bottom: 30px !important;
      padding-left: 15px;
      padding-right: 15px;
    }
  }
</style>
