<template>
  <div class="container">
    <button @click="changeTab('AddToDo')">Add</button>
    <button @click="changeTab('IncompletedToDos')">ToDo</button>
    <button @click="changeTab('CompletedTodo')">Complete</button>
    <keep-alive>
      <component
        :is="activeTab"
        :incompletedTodos="incompletedTodos"
        :completedTodos="completedTodos"
        @add-todo="addTodo"
        @complete-todo="completeTodo"
        @restore-todo="restoreToDo"
        @delete-todo="deleteTodo"
        ></component>
    </keep-alive>
  </div>
</template>

<script>
/* eslint-disable*/
import AddToDo from "./components/AddToDo";
import CompletedTodo from "./components/CompletedToDos";
import IncompletedToDos from "./components/IncompletedToDos";
import { todos } from "./data/todos";

export default {
  name: "app",
  data() {
    return {
      activeTab: "",
      todos,
      todoIncrementId: todos.length
    };
  },
  components: {
    AddToDo,
    IncompletedToDos,
    CompletedTodo
  },
  computed:{
    incompletedTodos(){
      return this.todos.filter(todo => todo.completed === false);
    },
    completedTodos(){
      return this.todos.filter(x => x.completed === true);
    }
  },
  methods: {
    changeTab(tabName) {
      this.activeTab = tabName;
    },
    addTodo(toDoName) {
      this.todos.push({
        id: this.todoIncrementId++,
        name: toDoName,
        completed: false
      });
    },
    restoreToDo(id){
      let currentTodo = this.getTodoId(id);
      currentTodo.completed = false;

    },
    completeTodo(id){
      let currentTodo = this.getTodoId(id);
      currentTodo.completed = true;
    },
    deleteTodo(id){    
    this.todos = this.todos.filter((el) => el.id !== id);
    },
     getTodoId(id){
      return this.todos.find(x => x.id === id);
    },
  }
};
</script>

<style>
/* Global Style */
body {
  background: #fff;
  color: #333;
  font-family: Lato, sans-serif;
}
.container {
  display: block;
  width: 400px;
  margin: 100px auto 0;
}
ul {
  margin: 0;
  padding: 0;
}
li * {
  float: left;
}
li,
h3 {
  clear: both;
  list-style: none;
}
input,
button {
  outline: none;
}
button {
  background: none;
  border: 0px;
  color: #888;
  font-size: 15px;
  width: 60px;
  margin: 10px 0 0;
  font-family: Lato, sans-serif;
  cursor: pointer;
}
button:hover {
  color: #333;
}
h3,
label[for="new-task"] {
  color: #333;
  font-weight: 700;
  font-size: 15px;
  border-bottom: 2px solid #333;
  padding: 30px 0 10px;
  margin: 0;
  text-transform: uppercase;
}
input[type="text"] {
  margin: 0;
  font-size: 18px;
  line-height: 18px;
  height: 18px;
  padding: 10px;
  border: 1px solid #ddd;
  background: #fff;
  border-radius: 6px;
  font-family: Lato, sans-serif;
  color: #888;
}
input[type="text"]:focus {
  color: #333;
}

/* Add Item  */

/* ToDo List */

/* Completed Tasks */
</style>


