<template>
    <input
        :value="modelValue"
        @input="updateInput"
        class="input"
        type="text"
    >
</template>

<script>
export default {
    name: 'ui-input',
    props: {
        modelValue: {
            type: [String, Number]
        }
    },
    methods: {
        updateInput(event) {
            this.$emit('update:modelValue', event.target.value)
        }
    }
}
</script>

<style scoped>
.input {
    width: 100%;
    border: 1px solid teal;
    background: none;
    padding: 10px 20px;
    font-family: "Times New Roman", sans-serif;
    font-size: 20px;
    border-radius: 5px;
    transition: all .3s ease;
}

.input:hover {
    border: 1px solid #074848;
    color: #043f3f;
}
</style>
