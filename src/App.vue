<template>
  <div class="main border border-muted rounded d-flex flex-column">
    <div class="container d-flex flex-row align-items-center justify-content-center p-3 bg-primary rounded">
      <h2 class="text-white container">{{page}}</h2>
      <TheNavigation @pickPage="pickPage" :tasks="tasksToSend" />
    </div>
    <router-view @newData="getData" @delItem="delItem" />
  </div>
</template>

<script>
import TheNavigation from '@/components/TheNavigation';

export default {
  components: {
    TheNavigation
  },
  data(){
    return{
      page: 'Home',
      tasks: [],
      tasksToSend: ''
    }
  },
  methods: {
    pickPage(p){
      this.page = p
    },
    getData(data){
      this.tasks.push(data)
      this.tasksToSend = JSON.stringify(this.tasks)
    },
    delItem(data){
      this.tasks.splice(data, 1)
      this.tasksToSend = JSON.stringify(this.tasks)
    }
  }
}
</script>

<style>
  * {
    box-sizing: border-box;
  }

  .main {
    height: 700px;
  }
</style>