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
            <a 
                class="delete text-danger p-3"
                @click="discardInput"
            >
                <i class="far fa-trash-alt"></i>
            </a>
        </td>  
    </tr>  
</template>

<script>
    import { BucketlistEventBus } from '../../main.js';

    export default {
        name: 'BucketlistItemCreate',
        methods: {
            discardInput() {
                BucketlistEventBus.$emit('closeNewItem');
            }
        }
    }
</script>

<style>
</style>