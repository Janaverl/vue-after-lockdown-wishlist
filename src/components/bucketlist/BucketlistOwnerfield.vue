<template>
    <div
        class="modal"
    >
        <div
            class="modal-dialog"
        >
            <div
                class="modal-content"
            >
                <div
                    class="modal-header"
                >
                    <h5
                        class="modal-title"
                    >
                        What's your name?
                    </h5>
                    <button
                        type="button"
                        class="close"
                        @click="closeModal()"
                    >
                        <span>&times;</span>
                    </button>
                </div>
                <div
                    class="modal-body"
                >
                <input
                    type="text"
                    :class="[
                        'form-control',
                        {'is-invalid': !nameIsvalid}
                    ]"
                    v-model="name"
                >
                </div>

                <div class="modal-footer">
                    <button 
                        type="button"
                        class="btn btn-success"
                        @click="closeModalAndSave(name)"
                    >
                        got it!
                    </button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import { BucketlistEventBus } from '../../main.js';

    export default {
        name: "BucketlistOwnerfield",
        data: function() {
            return {
                nameIsvalid: true,
                name: null
            };
        },
        methods: {
            isValidField(field){
                if(field == '' || field == null){
                    return false; 
                }
                return true;
            },
            closeModal() {
                BucketlistEventBus.$emit('exitModalName', name);
            },
            closeModalAndSave(name) {
                if(!this.isValidField(name)){
                    this.nameIsvalid = false;
                    return;
                }
                BucketlistEventBus.$emit('saveName', name);
            }
        }
    }
</script>

<style scoped>
    .modal {
        display: initial;
    }
</style>