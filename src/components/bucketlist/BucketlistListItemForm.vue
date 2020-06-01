<template>
    <tr>
        <td>
            <input
                type="text"
                :class="[
                    'form-control',
                    {'is-invalid': !isValid.name}
                ]"
                v-model="_this.item.name"
            >
        </td>
        <td>
            <input
                type="text"
                :class="[
                    'form-control',
                    {'is-invalid': !isValid.description}
                ]"
                v-model="_this.item.description"
            >
        </td>
        <td>
            <a class="add text-success p-3"
                @click="handleNewInput()"
            >
                <i class="far fa-plus-square"></i>
            </a>
            <a 
                class="delete text-danger p-3"
                @click="handleDiscardInput()"
            >
                <i class="far fa-trash-alt"></i>
            </a>
        </td>  
    </tr>  
</template>

<script>
    import { BucketlistEventBus } from '../../main.js';

    export default {
        name: 'BucketlistListItemForm',
        props: {
            _this: {
                type: Object,
                default: function () {
                    return {
                        item: {
                            name: '',
                            description: ''
                        },
                        index: null
                    };
                }
            },
        },
        data: function() {
            return {
                isValid: {
                    name: true,
                    description: true
                }
            }
        },
        methods: {
            handleDiscardInput() {
                if(this._this.index == null){
                    this.closeItem();
                    return;
                }
                this.removeItem(this._this.index);
            },
            handleNewInput() {
                this.validateItem(this._this.item, this.isValid);
                if(!this.isValid.name || !this.isValid.description){
                    return;
                }

                if(this._this.index == null){
                    this.addItem(this._this.item);
                    return;
                }

                this.replaceItem(this._this.item, this._this.index);
            },
            isValidField(field){
                if(field == '' || field == null){
                    return false; 
                }
                return true;
            },
            validateItem(item, validProp){
                validProp.name = this.isValidField(item.name);
                validProp.description = this.isValidField(item.description);
            }, 
            addItem(item) {
                BucketlistEventBus.$emit('addNewItem', item);
            },
            replaceItem(item, index) {
                BucketlistEventBus.$emit('replaceItem', {'item': item, 'index': index});
            },
            closeItem() {
                BucketlistEventBus.$emit('closeNewItem');
            },
            removeItem(index) {
                BucketlistEventBus.$emit('removeItemFromList', index);
            }
        }
    }
</script>

<style>
</style>