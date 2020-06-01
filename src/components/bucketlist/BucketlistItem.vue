<template>
    <tr>
        <td
            class="font-weight-bold"
        >
            {{ind+1}}. {{item.name}}
        </td>
        <td>
            {{item.description}}
        </td>
        <td>
            <a
                class="edit text-warning p-3"
            >
                <i class="far fa-edit"></i>
            </a>
            <a
                class="delete text-danger p-3"
                @click="removeItem(ind)"
            >
                <i class="far fa-trash-alt"></i>
            </a>
        </td>
    </tr>
</template>

<script>
    import { BucketlistEventBus } from '../../main.js';

    export default {
        name: 'BucketlistItem',
        props: {
            item: Object,
            ind: Number
        },
        methods: {
            removeItem(index) {
                BucketlistEventBus.$emit('removeItemFromList', index);
            }
        }
    }
</script>

<style>
</style>