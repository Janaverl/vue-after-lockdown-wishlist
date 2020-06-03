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
                class="btn btn-success add-new float-right"
                :disabled="disableAddNew"
                @click="startCreatingNewItem"
            >
                <i class="fa fa-plus"></i> Add New
            </button>
        </div>
    </div>
</template>

<script>
    import { BucketlistEventBus } from '../../main.js';

    export default {
        name: 'BucketlistHeader',
        data: function() {
            return {
                disableAddNew: false
            };
        },
        props: {
            title: String
        },
        methods: {
            startCreatingNewItem() {
                BucketlistEventBus.$emit('openNewItem');
            },

        },
        created() {
            BucketlistEventBus.$on('toggleNewButton', (disable) => {
                this.disableAddNew = disable;
            });
            BucketlistEventBus.$on('allowAdding', (isAllowedToAddNew) => {
                this.disableAddNew = !isAllowedToAddNew;
            });
        },
    }
</script>

<style>
</style>