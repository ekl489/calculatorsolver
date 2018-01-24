<template>
  <div id="app">
      <navbar></navbar><br>
      <div class="container content">
        <generator></generator>
      </div>
  </div>
</template>

<script>

import generator from './components/generator'
import navbar from './components/navbar'

export default {
  name: 'app',

  components: {
    generator,
    navbar
  },

  data () {
    return {

    }
  }

}
</script>

<style>

</style>
