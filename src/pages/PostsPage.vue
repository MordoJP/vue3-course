<template>
    <div>
        <h1>Page with posts</h1>
        <ui-input
            v-focus
            v-model="searchQuery"
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
                v-model="selectedSort"
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
        <!--        <div class="page__wrapper">-->
        <!--            <div-->
        <!--                v-for="pageNumber in totalPages"-->
        <!--                :key="pageNumber"-->
        <!--                class="page"-->
        <!--                :class="{-->
        <!--                    'page_active': page === pageNumber-->
        <!--                }"-->
        <!--                @click.stop="changePage(pageNumber)"-->
        <!--            >{{ pageNumber }}</div>-->
        <!--        </div>-->
    </div>
</template>

<script>
import PostForm from "@/components/PostForm";
import PostList from "@/components/PostList";
import axios from 'axios';

export default {
    components: {
        PostList,
        PostForm,
    },

    data() {
        return {
            posts: [],
            dialogVisible: false,
            isPostLoading: false,
            selectedSort: '',
            searchQuery: '',
            page: 1,
            limit: 10,
            totalPages: 0,
            sortOptions: [
                {value: 'title', name: 'by title'},
                {value: 'body', name: 'by body'},
            ]
        }
    },

    methods: {
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

        // changePage(pageNumber) {
        //     this.page = pageNumber
        //     this.fetchPosts()
        // },

        async fetchPosts() {
            try {
                this.isPostLoading = true
                const response = await axios.get('https://jsonplaceholder.typicode.com/posts', {
                    params: {
                        _page: this.page,
                        _limit: this.limit
                    }
                })
                this.totalPages = Math.ceil(response.headers['x-total-count'] / this.limit)
                this.posts = response.data
            } catch (e) {
                console.error('Error: ', e)
            } finally {
                this.isPostLoading = false
            }
        },

        async loadMorePosts() {
            try {
                this.page += 1
                const response = await axios.get('https://jsonplaceholder.typicode.com/posts', {
                    params: {
                        _page: this.page,
                        _limit: this.limit
                    }
                })
                this.totalPages = Math.ceil(response.headers['x-total-count'] / this.limit)
                this.posts = [...this.posts, ...response.data]
            } catch (e) {
                console.error('Error: ', e)
            }
        },
    },

    mounted() {
        this.fetchPosts()
    },

    computed: {
        sortedPosts() {
            return [...this.posts].sort((post1, post2) => post1[this.selectedSort]?.localeCompare(post2[this.selectedSort]))
        },

        sortedAndSearchPosts() {
            return this.sortedPosts.filter(post => post.title.toLowerCase().includes(this.searchQuery.toLowerCase()))
        }
    },
}
</script>

<style>
.app__btns {
    margin: 15px 0;
    display: flex;
    justify-content: space-between;
}

/*.page__wrapper {*/
/*    display: flex;*/
/*    margin-top: 15px;*/
/*    justify-content: center;*/
/*}*/

/*.page {*/
/*    border: 1px solid black;*/
/*    margin: 2px;*/
/*    padding: 8px;*/
/*}*/

/*.page_active {*/
/*    border: 2px solid teal;*/
/*    color: teal;*/
/*    background-color: #d7f5f5;*/
/*}*/

.observer {
    height: 30px;
    background-color: green;
}
</style>
