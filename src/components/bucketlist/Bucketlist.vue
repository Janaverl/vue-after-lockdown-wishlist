<template>
  <div class="row justify-content-center">
      <div class="col-sm-10 col-md-8 col-md-6 card">

        <bucketlist-header
          :title = bucketlistTitle
          :isNewActionAllowed = isNewActionAllowed
        ></bucketlist-header>

        <div class="card-body">

          <bucketlist-progressbar></bucketlist-progressbar>

          <bucketlist-list></bucketlist-list>

        </div>

      </diV>
    </div>
</template>

<script>
  import BucketlistHeader from './BucketlistHeader.vue'
  import BucketlistProgressbar from './BucketlistProgressbar.vue'
  import BucketlistList from './BucketlistList.vue'

  export default {
    name: 'Bucketlist',
    data: function() {
      return {
        bucketlistTitle: '10 things I will do when Lockdown COVID-19 is over.'
      };
    },
    components: {
      BucketlistHeader,
      BucketlistList,
      BucketlistProgressbar
    }
  }
</script>

<style>
</style>