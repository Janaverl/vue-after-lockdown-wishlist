<template>
    <table class="table table-bordered">
        <thead>
            <tr>
                <th style="width: 20%">name</th>
                <th style="width: 60%">description</th>
                <th style="width: 20%">Actions</th>
            </tr>
        </thead>
        <tbody>

            <bucketlist-item-form
                v-if="showInputForNew"
            ></bucketlist-item-form>

            <bucketlist-item
                v-for="(item, index) in items"
                :key="index"
                :item="item"
                :index="index"
            ></bucketlist-item>

        </tbody>
    </table>
</template>

<script>
    import BucketlistItem from './BucketlistItem.vue'
    import BucketlistItemForm from './BucketlistItemForm.vue'
    import { BucketlistEventBus } from '../../main.js';

    export default {
        name: 'BucketlistTable',
        data: function() {
            return {
                items: [
                    {
                        name: 'example 1',
                        description: 'Mijn goede vriendin Jana uitnodigen voor een BBQ.',
                    },
                    {
                        name: 'example 2',
                        description: 'een avondje doorzakken op café',
                    }
                ],
                showInputForNew: false
            }
        },
        methods: {
            isCreatingNewItem(isCreating) {
                BucketlistEventBus.$emit('toggleNewButton', isCreating);
                this.showInputForNew = isCreating;
            }
        },
        created() {
            const vm = this;

            BucketlistEventBus.$on('openNewItem', () => {
                vm.isCreatingNewItem(true);
            });
            BucketlistEventBus.$on('closeNewItem', () => {
                vm.isCreatingNewItem(false);
            });
            BucketlistEventBus.$on('addNewItem', (data) => {
                const itemToAdd = Object.assign({}, data);
                vm.items.unshift(itemToAdd);
                vm.isCreatingNewItem(false);
            });
            BucketlistEventBus.$on('replaceItem', (data) => {
                const itemToAdd = Object.assign({}, data.item);
                console.log(itemToAdd);
                vm.items.splice(data.ind, 1, itemToAdd);
            });
            BucketlistEventBus.$on('removeItemFromList', (index) => {
                vm.items.splice(index, 1);
            });
        },
        components: {
            BucketlistItem,
            BucketlistItemForm
        }
    }
</script>

<style>
</style>