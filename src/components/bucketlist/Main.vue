<template>
  <div class="row justify-content-center">
      <div class="col-sm-10 col-md-8 col-md-6 card">
        <bucketlist-header
          :title = bucketlistTitle
        ></bucketlist-header>
        <bucketlist-table></bucketlist-table>
      </diV>
    </div>
</template>

<script>
  import BucketlistHeader from './BucketlistHeader.vue'
  import BucketlistTable from './BucketlistTable.vue'

  export default {
    name: 'Bucketlist',
    data: function() {
      return {
        bucketlistTitle: '10 things I will do when Lockdown COVID-19 is over.'
      };
    },
    components: {
      BucketlistHeader,
      BucketlistTable
    }
  }
</script>

<style>
</style>