<template>
    <div class="card-body">

        <progressbar></progressbar>

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
    import Progressbar from './Progressbar.vue'

    export default {
        name: 'BucketlistTable',
        components: {
            BucketlistItem,
            BucketlistItemCreate,
            Progressbar
        }
    }
</script>

<style>
</style>