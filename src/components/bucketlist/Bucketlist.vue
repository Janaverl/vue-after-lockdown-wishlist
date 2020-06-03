<template>
  <div class="row justify-content-center mb-5">
      <div class="col-sm-10 card">

        <bucketlist-header
          :title = bucketlistTitle
        ></bucketlist-header>

        <div class="card-body">

          <bucketlist-progressbar></bucketlist-progressbar>

          <bucketlist-list></bucketlist-list>

        </div>

      </diV>
      <bucketlist-maximum-modal v-if="showModal"
      ></bucketlist-maximum-modal>
    </div>
</template>

<script>
  import BucketlistHeader from './BucketlistHeader.vue'
  import BucketlistProgressbar from './BucketlistProgressbar.vue'
  import BucketlistList from './BucketlistList.vue'
  import BucketlistMaximumModal from './BucketlistMaximumModal.vue'
  import { BucketlistEventBus } from '../../main.js';

  import contentText from '../../assets/data/contentText.json';

  export default {
    name: 'Bucketlist',
    data: function() {
      return {
        bucketlistTitle: contentText.title,
        showModal: false
      };
    },
    created() {
      BucketlistEventBus.$on('allowAdding', (isAllowedToAddNew) => {
        this.showModal = !isAllowedToAddNew;
      });
      BucketlistEventBus.$on('closeModal', () => {
        this.showModal = false;
      });
    },
    components: {
      BucketlistHeader,
      BucketlistList,
      BucketlistProgressbar,
      BucketlistMaximumModal
    }
  }
</script>

<style>
</style>