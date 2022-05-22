<template>
    <div>
        <div v-if="postList.length" class="post-list">
            <h3>Post list</h3>
            <transition-group name="post-list">
                <post-item
                    :post="post"
                    v-for="post in postList"
                    :key="post.id"
                    @remove="$emit('remove', post)"
                />
            </transition-group>
        </div>
        <span v-else v-html="'Post list is empty'" />
    </div>
</template>

<script>
import PostItem from "@/components/PostItem";

export default {
    components: {
        PostItem
    },
    props: {
        postList: {
            type: Array,
            required: true,
            default: () => [],
        }
    }
}
</script>

<style scoped>
.post-list {
    display: inline-block;
    margin-right: 10px;
}

.post-list-enter-active,
.post-list-leave-active {
    transition: all 0.4s ease;
}

.post-list-enter-from,
.post-list-leave-to {
    opacity: 0;
    transform: translateX(130px);
}

.post-list-move {
    transition: transform 0.4s ease;
}
</style>
