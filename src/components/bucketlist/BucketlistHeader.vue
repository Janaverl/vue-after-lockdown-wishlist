<template>
    <div class="card-header row">
        <div class="col-sm-8">
            <h2 class="font-weight-bold">
                {{title}}
            </h2>
        </div>
        <div class="col-sm-4">
            <button type="button" class="btn btn-success add-new float-right">
                <i class="fa fa-plus"></i> Add New
            </button>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'BucketlistHeader',
        props: {
            title: String
        }
    }
</script>

<style>
</style>