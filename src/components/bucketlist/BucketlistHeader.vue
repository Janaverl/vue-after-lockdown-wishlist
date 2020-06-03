<template>
    <div class="card-header row">
        <div class="col-sm-8">
            <h2 class="font-weight-bold">
                {{title}}
            </h2>
        </div>
        <div class="col-sm-4">
            <button
                type="button"
                class="btn btn-success btn-block"
                :disabled="disableAddNew"
                @click="startCreatingNewItem"
            >
                <i class="fa fa-plus"></i> Add New
            </button>
            <button v-if="!nameIsset"
                type="button"
                class="btn btn-success btn-block"
                @click="startAddingName"
            >
                <i class="fa fa-plus"></i> Add Your Name
            </button>
        </div>
        <bucketlist-ownerfield v-if="showModalOwner"
        ></bucketlist-ownerfield>
    </div>
</template>

<script>
    import BucketlistOwnerfield from './BucketlistOwnerfield.vue';
    import { BucketlistEventBus } from '../../main.js';

    export default {
        name: 'BucketlistHeader',
        data: function() {
            return {
                disableAddNew: false,
                showModalOwner: false
            };
        },
        props: {
            title: String,
            nameIsset: Boolean
        },
        watch: {

        },
        methods: {
            startCreatingNewItem() {
                BucketlistEventBus.$emit('openNewItem');
            },
            startAddingName() {
                this.showModalOwner = true;
            }
        },
        created() {
            BucketlistEventBus.$on('toggleNewButton', (disable) => {
                this.disableAddNew = disable;
            });
            BucketlistEventBus.$on('allowAdding', (isAllowedToAddNew) => {
                this.disableAddNew = !isAllowedToAddNew;
            });
            BucketlistEventBus.$on('saveName', () => {
                this.nameIsset = true;
                this.showModalOwner = false;
            });
            BucketlistEventBus.$on('exitModalName', () => {
                this.showModalOwner = false;
            });
        },
        components: {
            BucketlistOwnerfield
        }
    }
</script>

<style>
</style>