<template>
    <div>
        <div
            class="progress card-title"
        >
            <div
                class="progress-bar progress-bar-striped bg-success"
                :style="{width: percentage +'%'}"
            >
                    {{counter}}
            </div>
        </div>
    </div>
</template>

<script>
    import { BucketlistEventBus } from '../../main.js';
    
    export default {
        name: 'BucketlistProgressbar',
        data: function() {
            return {
                counter: 2,
                percentage: 20,
                isAddingAllowed: true
            };
        },
        methods: {
            hasReachedMaximum(counter, max = 10) {
                if(counter >= max){
                    return true;
                }
                return false;
            }
        },
        watch: {
            counter: function (value) { 
                this.percentage = (value * 10);
                this.isAddingAllowed = !this.hasReachedMaximum(this.counter);
            },
            isAddingAllowed: function(isAllowed) {
                BucketlistEventBus.$emit('allowAdding', isAllowed);
            }
        },
        created() {
            const vm = this;

            BucketlistEventBus.$on('addNewItem', () => {
                if(!vm.isAddingAllowed){
                    BucketlistEventBus.$emit('hasReachedMaximum');
                    return;
                }
                vm.counter = vm.counter + 1;
            });
            
            BucketlistEventBus.$on('removeItemFromList', () => {
                if(this.counter <= 0){
                    return;
                }
                vm.counter = vm.counter - 1;
            });
        }
    }
</script>

<style>
</style>