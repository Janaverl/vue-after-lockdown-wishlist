<template>
  <div id="app">

    <app-header 
      :appTitle = appTitle
    ></app-header>

    <app-content></app-content>

    <app-footer
      :name = createdBy.name
      :website = createdBy.website
    ></app-footer>
    
  </div>
</template>

<script>
import AppHeader from './components/AppHeader.vue'
import AppContent from './components/AppContent.vue'
import AppFooter from './components/AppFooter.vue'

export default {
  name: 'App',
  data: function() {
      return {
        appTitle: 'After lockdown bucketlist',
        createdBy: {
          name: 'Jana Verlinde',
          website: 'https://www.janaverlinde.be/'
        },
      };
  },
  components: {
    AppHeader,
    AppContent,
    AppFooter
  }
}
</script>

<style>
</style>
