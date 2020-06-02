<template>
    <tr v-if="!isBeingReplaced">
        <td
            class="font-weight-bold"
        >
            {{item.name}}
        </td>
        <td>
            {{item.description}}
        </td>
        <td>
            <a
                class="edit text-warning p-3"
                @click="startEditItem()"
            >
                <i class="far fa-edit"></i>
            </a>
            <a
                class="delete text-danger p-3"
                @click="removeItem(index)"
            >
                <i class="far fa-trash-alt"></i>
            </a>
        </td>
    </tr>
    <bucketlist-list-item-form v-else
        :_this="{
                item: {name: item.name, description: item.description},
                index: index
            }"
    ></bucketlist-list-item-form>
</template>

<script>
    import BucketlistListItemForm from './BucketlistListItemForm.vue'
    import { BucketlistEventBus } from '../../main.js';

    export default {
        name: 'BucketlistListItemRow',
        props: {
            item: Object,
            index: Number
        },
        data: function() {
            return {
                isBeingReplaced: false,
            }
        },
        methods: {
            disableNewButton(){
                BucketlistEventBus.$emit('toggleNewButton', true);
            },
            enableNewButton(){
                BucketlistEventBus.$emit('toggleNewButton', false);
            },
            leaveFormFormat(){
                this.isBeingReplaced = false;
            },
            openFormFormat(){
                this.isBeingReplaced = true;
            },
            removeItem(index) {
                BucketlistEventBus.$emit('removeItemFromList', index);
            },
            startEditItem() {
                this.disableNewButton();
                this.openFormFormat();
            }
        },
        created() {
            const vm = this;

            BucketlistEventBus.$on('replaceItem', () => {
                vm.enableNewButton();
                vm.leaveFormFormat();
            });
            
            BucketlistEventBus.$on('removeItemFromList', () => {
                vm.enableNewButton();
                vm.leaveFormFormat();
            });
        },
        components: {
            BucketlistListItemForm
        }
    }
</script>
²
<style>
</style>