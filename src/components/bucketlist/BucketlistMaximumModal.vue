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
                        {{title}}
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
                    <p>{{text}}</p>
                </div>

                <div class="modal-footer">
                    <button 
                        type="button"
                        class="btn btn-success"
                        @click="closeModal()"
                    >
                        {{confirmText}}
                    </button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import { BucketlistEventBus } from '../../main.js';

    import contentText from '../../assets/data/contentText.json';

    export default {
        name: "BucketlistMaximumModal",
        data: function() {
            const json = contentText.warnings.reachedMaximum;
            
            return {
            title: json.title,
            text: json.text,
            confirmText: json.confirmText
            };
        },
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
