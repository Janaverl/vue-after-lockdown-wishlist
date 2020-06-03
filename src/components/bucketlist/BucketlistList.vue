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

            <bucketlist-list-item-form v-if="showEmptyInput"
            ></bucketlist-list-item-form>

            <bucketlist-list-item-row v-for="(item, index) in items"
                :key="index"
                :item="item"
                :index="index"
            ></bucketlist-list-item-row>

        </tbody>
    </table>
</template>

<script>
    import BucketlistListItemRow from './BucketlistListItemRow.vue'
    import BucketlistListItemForm from './BucketlistListItemForm.vue'
    import { BucketlistEventBus } from '../../main.js';

    export default {
        name: 'BucketlistList',
        data: function() {
            return {
                items: [],
                showEmptyInput: null
            }
        },
        methods: {
            copyObject(data){
                return Object.assign({}, data);
            },
            disableNewButton(){
                BucketlistEventBus.$emit('toggleNewButton', true);
            },
            enableNewButton(){
                BucketlistEventBus.$emit('toggleNewButton', false);
            },
            closeNewItem(){
                this.showEmptyInput = false;
            },
            openNewItem(){
                this.showEmptyInput = true;
            }
        },
        mounted() {
            const vm = this;

            if (localStorage.myBucketlist) {
                var jsonString = localStorage.getItem("myBucketlist");
                vm.items = JSON.parse(jsonString);
            }
            
            if(vm.items.length == 0) {
                vm.openNewItem();
                vm.disableNewButton();
            } else {
                vm.closeNewItem();
                vm.enableNewButton();
            }

            vm.$root.$emit('getInputsLength', vm.items.length);
        },
        watch: {
            items(items) {
                localStorage.setItem("myBucketlist", JSON.stringify(items));
            }
        },
        created() {
            const vm = this;

            BucketlistEventBus.$on('openNewItem', () => {
                vm.openNewItem();
                vm.disableNewButton();
            });
            
            BucketlistEventBus.$on('closeNewItem', () => {
                vm.closeNewItem();
                vm.enableNewButton();
            });

            BucketlistEventBus.$on('addNewItem', (data) => {
                const newItem = this.copyObject(data);
                vm.items.unshift(newItem);
                vm.closeNewItem();
                vm.enableNewButton();
            });

            BucketlistEventBus.$on('replaceItem', (data) => {
                const newItem = this.copyObject(data.item);
                vm.items.splice(data.index, 1, newItem);
            });

            BucketlistEventBus.$on('removeItemFromList', (index) => {
                vm.items.splice(index, 1);
            });
        },
        components: {
            BucketlistListItemRow,
            BucketlistListItemForm
        }
    }
</script>

<style>
</style>