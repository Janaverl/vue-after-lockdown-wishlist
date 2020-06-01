<template>
    <tr>
        <td>
            <input
                type="text"
                :class="[
                    'form-control',
                    {'is-invalid': isInvalid.name}
                ]"
                v-model="newItem.name"
            >
        </td>
        <td>
            <input
                type="text"
                :class="[
                    'form-control',
                    {'is-invalid': isInvalid.name}
                ]"
                v-model="newItem.description"
            >
        </td>
        <td>
            <a class="add text-success p-3"
                @click="handleInput()"
            >
                <i class="far fa-plus-square"></i>
            </a>
            <a 
                class="delete text-danger p-3"
                @click="discardInput()"
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
        data: function() {
            return {
                newItem: {
                    name: '',
                    description: ''
                },
                isInvalid: {
                    name: false,
                    description: false
                }
            }
        },
        methods: {
            discardInput() {
                BucketlistEventBus.$emit('closeNewItem');
            },
            handleInput() {
                this.validateItem(this.newItem, this.isInvalid);
                if(this.isInvalid.name || this.isInvalid.description){
                    return;
                }
                this.addItem(this.newItem);
            },
            isValidField(field){
                console.log(field);
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
            }
        }
    }
</script>

<style>
</style>