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
        <button
            @click = "counter++"
        >
            increase
        </button>
        <button
            @click = "counter--"
        >
            decrease
        </button>
    </div>
</template>

<script>
    export default {
        name: 'Progressbar',
        data: function() {
            return {
                counter: 2,
                percentage: 20
            };
        },
        watch: {
            counter: function (value) { 
                this.percentage = (value * 10);
            }
        },
    }
</script>

<style>
</style>