<template>
    <div v-if="ifEmpty" class="container d-flex justify-content-center align-items-center">
        <h2 class="text-muted">No tasks</h2>
    </div>
    <div v-else>
        <div v-for="(item, key) in tasks" :key="key" class="container d-flex flex-row align-items-center justify-content-start">
            <h5 class="text-muted">{{key}}:</h5>
            <div class="container d-flex flex-row justify-centent-between align-items-center">
                <h2>{{item.name}}</h2>
                <p class="container d-flex align-items-center justify-content-start m-0">{{item.description}}</p>
            </div>
            <div class="container text-end">
                <div id="id" @click="del(key)">x</div>
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