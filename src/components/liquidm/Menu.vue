<template>
  <div>

    <h1>LiquidM</h1>
    <a href="https://platform.liquidm.com/login">
      Self-Service DSP
    </a>
    <h3>GitHub Followers</h3>

  </div>
</template>

<script>

    export default {
        name: 'Menu',
        props: {
            username: String
        },
        data () {
            return {
                username: '',
                results: '',
                error: '',
                loading: false,
            }
        },
        watch: {
        },
        methods:  {
        }
    }
</script>

<style>
*
{
text-align: center !important;
margin: auto !important;
}
</style>
