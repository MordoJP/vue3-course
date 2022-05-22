<template>
    <form @submit.prevent>
        <h4>creating post</h4>
        <ui-input
            v-focus
            v-model="post.title"
            class="input"
            type="text"
            placeholder="title"
        />
        <ui-input
            v-model="post.body"
            class="input"
            type="text"
            placeholder="body"
        />
        <ui-button
            class="btn"
            @click="createPost"
        >
            Create</ui-button>
    </form>
</template>

<script>
export default {
    data() {
        return {
            post: {
                title: '',
                body: '',
            }
        }
    },
    methods: {
        createPost() {
            this.post.id = Date.now()
            this.$emit('create', this.post)
            this.post = {
                title: '',
                body: '',
            }
        }
    },
}
</script>

<style scoped>
form {
    display: flex;
    flex-direction: column;
}

.input {
    margin-top: 15px;
}

.btn {
    margin-top: 15px;
    align-self: flex-end;
}
</style>
