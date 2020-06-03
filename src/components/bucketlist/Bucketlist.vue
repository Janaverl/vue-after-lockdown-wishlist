<template>
  <div class="row justify-content-center mb-5">
      <div class="col-sm-10 card">

        <bucketlist-header
          :title = bucketlistTitle
          :nameIsset = "owner == 'I' ? false : true"
        ></bucketlist-header>

        <div class="card-body">

          <bucketlist-progressbar></bucketlist-progressbar>

          <bucketlist-list></bucketlist-list>

        </div>

      </diV>
      <bucketlist-maximum-modal v-if="showModalMaximum"
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
        preTitle: contentText.title['pre'],
        owner: contentText.owner,
        afterTitle: contentText.title['after'],
        bucketlistTitle: '',
        showModalMaximum: false
      };
    },
    methods: {
      setTitle() {
        this.bucketlistTitle = `${this.preTitle} ${this.owner} ${this.afterTitle}`;
      }
    },
    watch: {
      owner() {
        this.setTitle();
      }
    },
    mounted() {
      const vm = this;
      if (localStorage.ownerBucketlist) {
        var jsonString = localStorage.getItem("ownerBucketlist");
        vm.owner = JSON.parse(jsonString);
      }
      this.setTitle();
    },
    created() {
      BucketlistEventBus.$on('allowAdding', (isAllowedToAddNew) => {
        this.showModalMaximum = !isAllowedToAddNew;
      });
      BucketlistEventBus.$on('closeModal', () => {
        this.showModalMaximum = false;
      });
      BucketlistEventBus.$on('saveName', (name) => {
        this.owner = name;
        localStorage.setItem("ownerBucketlist", JSON.stringify(name));
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