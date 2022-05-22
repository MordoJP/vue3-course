<template>
    <div>
        <h1>Page with posts</h1>
        <ui-input
            v-focus
            :model-value="searchQuery"
            @update:model-value="setSearchQuery"
            placeholder="search..."
        />
        <div class="app__btns">
            <ui-button
                class="create-btn"
                @click="openDialog"
            >
                Create post
            </ui-button>
            <ui-select
                :model-value="selectedSort"
                @update:model-value="setSelectedSort"
                :options="sortOptions"
            />
        </div>
        <ui-dialog v-model:show="dialogVisible">
            <post-form
                @create="createPost"
            />
        </ui-dialog>
        <post-list
            :post-list="sortedAndSearchPosts"
            @remove="removePost"
            v-if="!isPostLoading"
        />
        <div v-else>Data loading . . . . .</div>
        <div v-intersection="loadMorePosts" class="observer"></div>
    </div>
</template>

<script>
import PostForm from "@/components/PostForm";
import PostList from "@/components/PostList";
import { mapActions, mapGetters, mapMutations, mapState } from 'vuex'

export default {
    components: {
        PostList,
        PostForm,
    },

    data() {
        return {
            dialogVisible: false,
        }
    },

    methods: {
        ...mapMutations({
            setPage: 'post/setPage',
            setSearchQuery: 'post/setSearchQuery',
            setSelectedSort: 'post/setSelectedSort'
        }),
        ...mapActions({
            loadMorePosts: 'post/loadMorePosts',
            fetchPosts: 'post/fetchPosts'
        }),
        createPost(post) {
            this.posts.push(post)
            this.dialogVisible = false
        },

        removePost(post) {
            this.posts = [...this.posts.filter(p => p.id !== post.id)]
        },

        openDialog() {
            this.dialogVisible = true
        },
    },

    mounted() {
        this.fetchPosts()
    },

    computed: {
        ...mapState({
            posts: state => state.post.posts,
            isPostLoading: state => state.post.isPostLoading,
            selectedSort: state => state.post.selectedSort,
            searchQuery: state => state.post.searchQuery,
            page: state => state.post.page,
            limit: state => state.post.limit,
            totalPages: state => state.post.totalPages,
            sortOptions: state => state.post.sortOptions
        }),
        ...mapGetters({
            sortedPost: 'post/sortedPosts',
            sortedAndSearchPosts: 'post/sortedAndSearchPosts'
        }),
    },
}
</script>

<style>
.app__btns {
    margin: 15px 0;
    display: flex;
    justify-content: space-between;
}

.observer {
    height: 30px;
    background-color: green;
}
</style>
