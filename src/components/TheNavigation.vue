<template>
    <div class="container text-end">
        <router-link :to="{name: 'Home'}" class="links" @click="pickPage('Home')">Home</router-link> |
        <router-link :to="{name: 'Menu', params: {data: tasks}}" class="links" @click="pickPage('Menu')">Menu</router-link>
    </div>
</template>

<script>
    export default {
        props: {
            tasks: {
                type: String
            }
        },
        methods: {
            pickPage(p) {
                this.$emit('pickPage', p)
            }
        },
        emits: ['pickPage']
    }
</script>

<style scoped>
    a.links {
        color: #fff;
        font-weight: 600;
        text-decoration: none;
    }

    a.router-link-active {
        color: rgb(255, 213, 134)
    }
</style>