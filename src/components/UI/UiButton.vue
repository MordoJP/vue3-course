<template>
    <button class="btn">
        <slot />
    </button>
</template>

<script>
export default {
    name: 'ui-button'
}
</script>

<style scoped>
.btn:hover {
    border: 1px solid #074848;
    color: #043f3f;
}

.btn {
    transition: all .3s ease;
    padding: 10px 20px;
    border: 1px solid teal;
    background: none;
    border-radius: 5px;
    font-family: "Times New Roman", sans-serif;
    font-size: 20px;
    color: #28bebe;
    cursor: pointer;
}
</style>
