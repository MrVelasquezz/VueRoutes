<template>
    <div v-if="ifEmpty" class="container d-flex justify-content-center align-items-center">
        <h2 class="text-muted">No tasks</h2>
    </div>
    <div v-else>
        <div v-for="(item, key) in tasks" :key="key" class="container d-flex flex-row align-items-center justify-content-start">
            <h5 class="text-muted">{{key}}:</h5>
            <div class="container d-flex flex-row justify-centent-between align-items-center">
                <h2 class="container">{{item.name}}</h2>
                <p class="container d-flex align-items-center justify-content-start m-0">{{item.description}}</p>
            </div>
            <div>
                <div id="closeBtn" @click="del(key)">
                    <img src="@/assets/times-solid.svg" id="close" alt="">
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'Menu',
        data() {
            return {
                tasks: ''
            }
        },
        created() {
            if (this.$route.params.data) {
                this.tasks = JSON.parse(this.$route.params.data)
            }
        },
        methods:{
            del(key){
                this.tasks.splice(key, 1)
                this.$emit('delItem', key)
            }
        },
        computed: {
            ifEmpty(){
                if(this.tasks.length != 0){
                    return false
                }
                else{
                    return true
                }
            }
        },
        emits: ['delItem']
    }
</script>

<style scoped>
    #close{
        width: 20px;
        cursor: pointer;
    }
    h2.container{
        min-width:min-content;
        max-width: max-content;
    }
</style>