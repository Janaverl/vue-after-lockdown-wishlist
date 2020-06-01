<template>
    <div class="card-body">
        <div class="progress card-title">
            <div class="progress-bar progress-bar-striped bg-success" style="width: 10%">
                1
            </div>
        </div>
        <table class="table table-bordered">
            <thead>
                <tr>
                    <th style="width: 20%">name</th>
                    <th style="width: 60%">description</th>
                    <th style="width: 20%">Actions</th>
                </tr>
            </thead>
            <tbody>
                <bucketlist-item></bucketlist-item>  
                <bucketlist-item-create></bucketlist-item-create>  
            </tbody>
        </table>
    </div>
</template>

<script>
    import BucketlistItem from './BucketlistItem.vue'
    import BucketlistItemCreate from './BucketlistItemCreate.vue'


    export default {
        name: 'BucketlistTable',
        components: {
            BucketlistItem,
            BucketlistItemCreate,
        }
    }
</script>

<style>
</style>