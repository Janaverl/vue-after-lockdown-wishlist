<template>
    <tr>
        <td>
            <input type="text" class="form-control" name="name">
        </td>
        <td>
            <input type="text" class="form-control" name="description">
        </td>
        <td>
            <a class="add text-success p-3">
                <i class="far fa-plus-square"></i>
            </a>
            <a class="delete text-danger p-3">
                <i class="far fa-trash-alt"></i>
            </a>
        </td>  
    </tr>  
</template>

<script>
    export default {
        name: 'BucketlistItemCreate',
        props: {
            title: String
        }
    }
</script>

<style>
</style>