<template>
  <v-app
    id="campaigns"
    dark>

  </v-app>
</template>

<script>
export default {
  name: 'campaigns',
  metaInfo () {
    return {
      title: 'LiquidM - Campaigns'
    }
  },
  data () {
    return {
      username: '',
      results: '',
      error: '',
      loading: false,
      option: 'campaigns',
    }
  },
  components: {
  }
}
</script>

<style>
</style>