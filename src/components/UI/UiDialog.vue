<template>
    <div class="dialog" v-if="show" @click="hideDialog">
        <div @click.stop class="dialog__content">
            <slot />
        </div>
    </div>
</template>

<script>
import toggleMixin from "@/mixins/toggleMixin";

export default {
    name: 'ui-dialog',
    mixins: [toggleMixin]
}
</script>

<style scoped>
.dialog {
    top: 0;
    bottom: 0;
    right: 0;
    left: 0;
    background-color: rgb(0, 0, 0, .5);
    position: fixed;
    display: flex;
    min-width: 300px;
    min-height: 100px;
}

.dialog__content {
    margin: auto;
    background-color: white;
    border-radius: 20px;
    padding: 20px;
}
</style>
