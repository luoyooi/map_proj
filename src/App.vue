<template>
  <div id="app">
    <header-show></header-show>
    <map-show></map-show>
  </div>
</template>

<script>
import Header from './components/header.vue'
import Map from './components/map.vue'

export default {
  el: 'app',
  data: function () {
    return {

    }
  },
  components: {
    'header-show': Header,
    'map-show': Map
  }
}
</script>
