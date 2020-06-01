<template>
    <tr>
        <td>
            <input
                type="text"
                :class="[
                    'form-control',
                    {'is-invalid': isInvalid.name}
                ]"
                v-model="_this.item.name"
            >
        </td>
        <td>
            <input
                type="text"
                :class="[
                    'form-control',
                    {'is-invalid': isInvalid.description}
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
        name: 'BucketlistItemForm',
        props: {
            _this: {
                type: Object,
                default: function () {
                    return {
                        item: {
                            name: '',
                            description: ''
                        },
                        status: 'add',
                        index: null
                    };
                }
            },
        },
        data: function() {
            return {
                isInvalid: {
                    name: false,
                    description: false
                }
            }
        },
        methods: {
            handleDiscardInput() {
                if(this._this.index == null){
                    this.closeItem();
                    return;
                }
                console.log('just did handleDiscardInput in Form');
                this.removeItem(this._this.index);
            },
            handleNewInput() {
                this.validateItem(this._this.item, this.isInvalid);
                if(this.isInvalid.name || this.isInvalid.description){
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
            validateItem(item, invalidProp){
                invalidProp.name = !this.isValidField(item.name);
                invalidProp.description = !this.isValidField(item.description);
            }, 
            addItem(item) {
                BucketlistEventBus.$emit('addNewItem', item);
            },
            replaceItem(item, ind) {
                BucketlistEventBus.$emit('replaceItem', {'item': item, 'ind': ind});
            },
            closeItem() {
                BucketlistEventBus.$emit('closeNewItem');
            },
            removeItem(ind) {
                BucketlistEventBus.$emit('removeItemFromList', ind);
            }
        }
    }
</script>

<style>
</style>