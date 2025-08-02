<template>
  <app-header></app-header>
  <main>
   <add-todo @AddnewTodo="AddToDo"></add-todo>
    <ul class="todos">
     <todo-item v-for="item in todos" :key="item.id" :todo="item" @Deleted="deleteTodo" @changeStatus="changeTodoStatus"></todo-item>       
    </ul>
    <app-filter @deleteAllCompleted = "deleteAllCompleted"></app-filter>
  </main>
    <app-footer></app-footer>
</template>

<script>
import AppHeader from './components/AppHeader.vue';
import AppFooter from './components/AppFooter.vue';
import AddTodo from './components/AddTodo.vue';
import TodoItem from './components/ToDo.vue';
import AppFilter from './components/AppFilter.vue';
export default {
  name: 'App',
  components: {
    AppHeader,
    AppFooter,
    AddTodo,
    TodoItem,
    AppFilter,
  },
  data(){
    return{
      todos : []
    }
  },
  methods:{
    AddToDo(title){
      const id = Math.random().toString(16).slice(2)
      const todo = {id ,title , isCompleted : false}
      this.todos.push(todo)
    },
    deleteTodo(id){
      this.todos = this.todos.filter((todo)=>{
        return todo.id !== id
      })
    },
    changeTodoStatus(id,newStatus){
      let newTodos = [...this.todos];
      let selectedTodo = newTodos.find(item=>item.id === id)
      selectedTodo.isCompleted = newStatus
      this.todos = newTodos;
    },
    deleteAllCompleted(){
      if(confirm("ایا ا پاک کردن تمامی تکمیل شده ها مطمئن هستید؟")){
      let newTodos = [...this.todos];
      newTodos = newTodos.filter(f =>f.isCompleted === false);
      this.todos = newTodos
      }
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
