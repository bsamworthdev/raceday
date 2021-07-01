<template>
    <input class="text-yellow-amstrad text-xl" :value="modelValue" @input="$emit('update:modelValue', $event.target.value)" ref="input">
</template>
<style scoped>
    input{
        border:none!important;
        background-color:transparent;
    }
</style>
<script>
    export default {
        props: ['modelValue'],

        emits: ['update:modelValue'],

        methods: {
            focus() {
                this.$refs.input.focus()
            }
        }
    }
</script>

