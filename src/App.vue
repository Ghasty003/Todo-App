<template>

<div class="container">
  <p><img src="images/todo1.png" alt="image"></p>

  <div class="todoContainer">
    <h1 class="todo"> <i class="fas fa-clipboard-check"></i> {{message}} </h1>
    <h2 v-html="addMessage" class="todoh2"></h2>

    <p class="todoP"> You have added {{ allTask }} {{items.length > 1 ? 'tasks' : 'task'}}  at the moment. </p>

    <input type="text" placeholder="I need to..." v-model="newTask" class=".input">
    <button :disabled=" newTask.length < 1" @click="addTask">Add task</button>

    <div v-if="newTask" class="tasks">
      <h2> New task preview: </h2>
      <p> {{newTask}} </p>
    </div>

    <ul>
      <li v-show="item.cutOut" v-for="(item) in latest" :key="item.id" :class="{strikeOut:item.isDone}" >
        <p>{{item.task.toUpperCase()}}</p> <span> <input type="checkbox" @click="strikeItem(item)"> <i  class="fa fa-trash-o" @click="deleteItem(item)"></i></span>
      </li>
    </ul>
  </div>

  <p><img src="images/todo2.png" alt="image"></p>
</div>

</template>

<script>

export default {
  data () {
    return {
      message: 'To-do list',
      addMessage: '<p>Add a new task</p>',
      newTask: '',
      items: [
      ]
    }
  },
  methods: {
    addTask () {
      if (this.newTask < 1) return
      this.items.push({ id: this.items.length, task: this.newTask, isDone: false, cutOut: true })
      this.newTask = ''
    },
    deleteItem (item) {
      item.cutOut = false
      return this.allTask--
    },
    strikeItem (item) {
      item.isDone = true
    }
  },
  computed: {
    allTask () {
      return this.items.length
    },
    latest () {
      return [...this.items]
    }
  }
}
// alert(innerWidth)

</script>

<style>

body{
  background-color: darkslateblue;
  font-family: 'Truculenta';
}

.container{
  display: flex;
  justify-content: space-around;
  position: relative;
}

.todoContainer{
  position: relative;
  top: 20%;
}

.todo{
  color: white;
  font-size: 40px;
}

.todoh2{
  font: 35px;
  color: navajowhite;
}

.todoP{
  font-size: large;
  color: peru;
}

img{
  width: 250px;
  height: 400px;
  position: relative;
  animation-name: animate;
  animation-duration: 4s;
  z-index: -1;
}

@keyframes animate{
  0%{
    transform: translateY(-100px);
  }
  50%{
    transform: translateY(0px);
  }
  75%{
    transform: translateX(-100px);
  }
  100%{
    transform: translateX(0px);
  }
}

li{
  list-style: none;
  display: flex;
  justify-content: space-between;
  align-items: center;
  font-size: 17px;
  position: relative;
  margin: 10px;
  background-color: slateblue;
  left: -15%;
  width: 100%;
  height: 30px;
}

li:first-child{
  margin-top: 30px;
}

li p {
  position: relative;
  left: 10px;
  color: lavender;
}

.strikeOut{
  text-decoration: line-through;
}

.fa-trash-o{
  color: rgb(136, 21, 21);
  cursor: pointer;
}

.input{

  box-shadow: inset -6px -6px 13px #fff, inset 6px 6px 13px rgba(0, 0, 0, .16);
  outline: none;
  border: none;
  border-radius: 7px;
}

button{
  border: none;
  padding: 5px 15px;
  font-size: 15px;
  text-align: center;
  text-decoration: none;
  border-radius: 15px;
  box-shadow: 0 2px #dd5e89;
  background-color: rgb(181, 136, 226);
}

button:hover{
  background-color: #dd5e89;
}

button:active{
  box-shadow: 0 3px;
  transform: translateY(4px);
}

.tasks{
  color: lightblue;
}

@media screen and (max-width:785px) {
  img{
    width: 150px;
    height: 300px;
    top: 20%;
  }
}

@media screen and (max-width:590px) {
  .todo{
    font-size: 30px;
  }

  .todoh2 p{
    font-size: 20px;
  }

  .todoP{
    font-size: 16px;
  }

  button{
    padding: 1px 6px;
  }

  img{
  width: 100px;
}
}

@media screen and (max-width:400px) {
  img{
    width: 80px;
    height: 200px;
  }
}
</style>
