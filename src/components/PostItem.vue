<template>
    <div class="post">
        <div class="post__body">
            <div><strong>ID: </strong>{{ post.id }}</div>
            <div><strong>Title: </strong>{{ post.title }}</div>
            <div><strong>Description: </strong>{{ post.body }}</div>
        </div>
        <div class="post__btns">
            <ui-button
                class="post__btn"
                @click="$router.push(`/posts/${post.id}`)"
            >
                open
            </ui-button>
            <ui-button
                class="post__btn"
                @click="$emit('remove', post)"
            >
                delete
            </ui-button>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        post: {
            type: Object,
            required: true,
            default: () => ({})
        },
    },
}
</script>

<style scoped>
.post {
    padding: 15px;
    border: 2px solid teal;
    margin-top: 15px;
    border-radius: 5px;
    display: flex;
    align-items: center;
    justify-content: space-between;
}

.post__body {
    font-family: "Times New Roman", sans-serif;
    font-size: 20px;
}

.post__btns {
    display: flex;
}

.post__btn {
    margin-left: 15px;
}
</style>
