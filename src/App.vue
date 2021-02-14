<template>
  <div id="app">
    <converter></converter>
  </div>
</template>

<script>
import Converter from './components/Converter'
export default {
  name: 'App',
  components: {
    'converter': Converter
  }
}
</script>

<style>
@import './Style.css'

</style>
