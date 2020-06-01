<template>
  <div class="container">
    <bucketlist></bucketlist>
  </div>
</template>

<script>
  import Bucketlist from './bucketlist/Bucketlist.vue'

  export default {
    name: 'AppContent',
    components: {
      Bucketlist
    }
  }
</script>

<style>
</style>
