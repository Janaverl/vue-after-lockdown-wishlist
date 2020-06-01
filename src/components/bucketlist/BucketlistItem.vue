<template>
    <tr v-if="!isBeingReplaced">
        <td
            class="font-weight-bold"
        >
            {{index+1}}. {{item.name}}
        </td>
        <td>
            {{item.description}}
        </td>
        <td>
            <a
                class="edit text-warning p-3"
                @click="editItem()"
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
    <bucketlist-item-form v-else
        :_this="{
                item: {
                    name: item.name,
                    description: item.description
                },
                index: index
            }"
    ></bucketlist-item-form>
</template>

<script>
    import BucketlistItemForm from './BucketlistItemForm.vue'
    import { BucketlistEventBus } from '../../main.js';

    export default {
        name: 'BucketlistItem',
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
                console.log('just did removeItem in Item');
                console.log(index);
                BucketlistEventBus.$emit('removeItemFromList', index);
            },
            editItem() {
                this.disableNewButton();
                this.openFormFormat();
            }
        },
        created() {
            BucketlistEventBus.$on('replaceItem', () => {
                this.enableNewButton();
                this.leaveFormFormat();
            });
            BucketlistEventBus.$on('removeItemFromList', () => {
                this.enableNewButton();
                this.leaveFormFormat();
            });
        },
        components: {
            BucketlistItemForm
        }
    }
</script>
²
<style>
</style>