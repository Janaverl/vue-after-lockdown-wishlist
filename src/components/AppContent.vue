<template>
  <div class="container">
    <bucketlist></bucketlist>
  </div>
</template>

<script>
  import Bucketlist from './bucketlist/Main.vue'

  export default {
    name: 'AppContent',
    components: {
      Bucketlist
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
