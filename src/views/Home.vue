<template>
  <div class="container-fluid text-start">
    <h2>Main app</h2>
    <form class="d-flex flex-column">
      <div>
        <label class="form-lable text-muted">Name of task</label>
        <input type="text" class="form-control" v-model="taskNameData" maxlength="32">
        <div class="container text-end">{{nameCounter}}/32</div>
      </div>
      <div>
        <label class="form-lable text-muted">Task description</label>
        <textarea type="text" class="form-control" v-model="taskDescData" rows="5" maxlength="500"></textarea>
        <div class="container text-end">{{descCounter}}/500</div>
      </div>
    </form>
    <div class="d-flex justify-content-end">
        <button class="btn btn-primary px-5 py-2 me-3" @click="addTask" v-bind:disabled="isDisabled">Add task</button>
        <button class="btn btn-danger px-5 py-2" @click="clearTask">Clear fields</button>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src


export default {
  name: 'Home',
  components: {
    
  },
  data(){
    return{
      taskNameData: '',
      taskDescData: '',
      dis: false
    }
  },
  emits: ['newData'],
  methods: {
    addTask(){
      this.$emit('newData', {name: this.taskNameData, description: this.taskDescData})
      this.taskNameData = ''
      this.taskDescData = ''
    },
    clearTask(){
      this.taskNameData = ''
      this.taskDescData = ''
    }
  },
  computed: {
    nameCounter(){
      return 32 - this.taskNameData.length
    },
    descCounter(){
      return 500 - this.taskDescData.length
    },
    isDisabled(){
      if(this.taskNameData.length != 0 && this.taskDescData.length != 0){
        return false
      }
      else{
        return true
      }
    }
  }
}
</script>
