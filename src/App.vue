<template>
  <div id="app">
    <nav class="navbar navbar-light bg-light mb-5">
      <span class="navbar-brand">
        After lockdown bucketlist
      </span>
    </nav>
    <div class="container">
      <bucket-list></bucket-list>
    </div>
    <footer class="page-footer font-small blue fixed-bottom">
      <div class="text-center py-3">created by
        <a href="https://www.janaverlinde.be/"> Jana Verlinde</a>
      </div>
    </footer>
  </div>
</template>

<script>
import BucketList from './components/BucketList.vue'

export default {
  name: 'App',
  components: {
    BucketList
  }
}
</script>

<style>
</style>
