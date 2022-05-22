<template>
    <div>
        <h1>Page with Composition API</h1>
        <ui-input
            v-focus
            v-model="searchQuery"
            placeholder="search..."
        />
        <div class="app__btns">
            <ui-button
                class="create-btn"
            >
                Create post
            </ui-button>
            <ui-select
                v-model="selectedSort"
                :options="sortOptions"
            />
        </div>
        <ui-dialog v-model:show="dialogVisible">
            <post-form
            />
        </ui-dialog>
        <post-list
            :post-list="sortedAndSearchPosts"
            v-if="!isPostLoading"
        />
        <div v-else>Data loading . . . . .</div>
    </div>
</template>

<script>
import PostForm from "@/components/PostForm";
import PostList from "@/components/PostList";
import {ref} from 'vue'
import usePosts from "@/hooks/usePosts";
import useSortedPosts from "@/hooks/useSortedPosts";
import useSortedAndSearchPosts from "@/hooks/useSortedAndSearchedPosts";
export default {
    components: {
        PostList,
        PostForm,
    },

    data() {
        return {
            dialogVisible: false,
            sortOptions: [
                {value: 'title', name: 'by title'},
                {value: 'body', name: 'by body'},
            ]
        }
    },
    setup(props) {
        const {posts, totalPage, isPostLoading} = usePosts(10)
        const {sortedPosts, selectedSort} = useSortedPosts(posts)
        const {searchQuery, sortedAndSearchPosts} = useSortedAndSearchPosts(sortedPosts)

        return {
            posts,
            totalPage,
            isPostLoading,
            sortedPosts,
            selectedSort,
            searchQuery,
            sortedAndSearchPosts
        }
    }
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
