<template>
    <div class="navbar">
        <span
            class="navbar__title"
            @click="$router.push('/')"
        >Vue 3 test APP</span>
        <div class="navbar__btns">
            <ui-button
                class="navbar__btn"
                @click="$router.push('/posts')"
            >Posts</ui-button>
            <ui-button
                class="navbar__btn"
                @click="$router.push('/about')"
            >About app</ui-button>
            <ui-button
                class="navbar__btn"
                @click="$router.push('/store')"
            >Store</ui-button>
            <ui-button
                class="navbar__btn"
                @click="$router.push('/composition')"
            >Composition</ui-button>
        </div>
    </div>
</template>

<script>
export default {

}
</script>

<style scoped>
.navbar {
    height: 50px;
    background-color: teal;
    box-shadow: 2px 2px 4px #3b4d4d;
    display: flex;
    align-items: center;
    padding: 30px 50px;
}

.navbar__title {
    font-family: "Times New Roman", sans-serif;
    font-size: 30px;
    font-weight: bold;
    color: #28bebe;
    cursor: pointer;
    transition: all .3s ease;
}

.navbar__title:hover {
    color: #4fe5e5;
}

.navbar__btns {
    margin-left: auto;
}

.navbar__btn {
    margin-left: 15px;
}
</style>
