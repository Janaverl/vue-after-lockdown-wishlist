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
                        You've added 10 items.
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
                    <p>Let's hope we can go out soon to do all these amazing things!</p>
                </div>

                <div class="modal-footer">
                    <button 
                        type="button"
                        class="btn btn-success"
                        @click="closeModal()"
                    >
                        Got it!
                    </button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import { BucketlistEventBus } from '../../main.js';
    export default {
        methods: {
            closeModal() {
                BucketlistEventBus.$emit('closeModal');
            }
        }
    }
</script>

<style scoped>
.modal {
    display: initial;
}
</style>
