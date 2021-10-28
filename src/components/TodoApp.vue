<template>
  <div class="container">
    <h1>To DO List</h1>
    <p>Create your project task</p>
    <form>
      <input v-model="task" type="text" id="input-text" placeholder="inter your task">
      <button @click="addList()" type="button" id="addButton">Add</button>
    </form>
    <ul id="js__list" class="t_head">
    </ul>
    <table class="table table-striped table-dark" >
      <thead>
      <tr>
        <th scope="col">Task</th>
        <th scope="col">Status</th>
        <th scope="col" class="center">Edit</th>
        <th scope="col" class="center">Delete</th>
        <th scope="col" class="center">Strikeout</th>
      </tr>
      </thead>
      <tbody>
      <tr v-for="(task , index) in tasks" :key="index">
        <th style="width: 150px" class="center" >{{task.name}}</th>
        <td style="width: 150px">
          <span  @click="changeStatus(index)" class="pointer">{{ task.status }}</span>
        </td >
        <td style="width: 150px">
          <div class="pointer" @click="ediTask(index)">
            <span class="fas fa-pen"></span>
          </div>
        </td>
        <td style="width: 150px">
          <div class="pointer" @click="deleteTask(index)">
          <span class="fas fa-trash"></span>
          </div>
        </td>
        <td style="width:150px">
          <div class="pointer" @click="strikeOuTASK(index)">
            <span class="fas fa-strikethrough"></span>
          </div>
        </td>

      </tr>

      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: 'todolist',
  props: {
    msg: String
  },
  data(){
    return{
      task:'',
      editNumber:null,
      statuses:['in-progress', 'wait' , 'done'],
      tasks:[
        {
          name:'task-one',
          status:'wait'
        },
        {
          name:'task-two',
          status:'in-progress'
        },
      ]
    }
  },
  methods:{
    addList(){
     if(this.task.length===0) return;
     if(this.editNumber===null) {
       this.tasks.push({
         name: this.task,
         status: 'in-progress'
       })
     }
     else{
       this.tasks[this.editNumber].name = this.task
       this.editNumber = null
     }
      this.task = ''
    },
    deleteTask(index){
      this.tasks.splice(index , 1)
    },
    ediTask(index){
      this.task = this.tasks[index].name
      this.editNumber = index
    },
    changeStatus(index){
      let nextIndex = this.statuses.indexOf(this.tasks[index].status)
      if(++nextIndex > 2) {
        nextIndex = 0
      }
      this.tasks[index].status = this.statuses[nextIndex]
    },
    strikeOuTASK(index){
      this.task[index].classList.toggle('strikethrough');
    }
  }
};
</script>


<style scoped>
.container{
  display: flex;
  flex-direction: column;
  justify-content: center;
  text-align: center;
  margin-top: 15vh;
}
form{
  display: flex;
  justify-content:center;
  margin-top: 5vh;
}
form input{
  border: none;
  width: 30vw;
  height: 40px;
  line-height: 35px;
  border-radius: 6px;
  padding: 0 5px;
}
form button {
  width: 10%;
  margin-left: 10px;
  border-radius: 6px;
  border: none;
  color: #D4F1F4;
  background-color: #05445E;
}
table{
  margin-top: 20px;
}
.pointer{
  cursor: pointer;
}
.strikethrough{
  text-decoration: line-through;
}


</style>
