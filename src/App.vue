<template>
  <app-header></app-header>
  <main>
   <add-todo @AddnewTodo="AddToDo"></add-todo>
    <ul class="todos">
     <todo-item v-for="(item,i) in filteredTodos" :key="item.id" :todo="item" @Deleted="deleteTodo" @changeStatus="changeTodoStatus" @dragover.prevent @dragstart="dragstart(i)" @drop="drop(i)"></todo-item>       
    </ul>
    <app-filter @deleteAllCompleted = "deleteAllCompleted" :activeCount="ActiveTodoCount" @changeTab ="changeTabHandler" :activeTab="activeTab"></app-filter>
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
      todos : [],
      draggging : -1,
      activeTab:"all",
    }
  },
  methods:{
    AddToDo(title){
      if(!title){
      this.$toast.error("لطفا متن تودو را پر کنید")
      }
      else{
      const id = Math.random().toString(16).slice(2)
      const todo = {id ,title , isCompleted : false}
      this.todos.push(todo)
      this.$toast.success("تودو جدید اضافه شد")
      }

    },
    deleteTodo(id){
      const todo = this.todos.find(todo=>todo.id == id)
      this.todos = this.todos.filter(todo=>todo.id !== id)
      this.$toast.error(`${todo.title} حذف شد`)
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
       this.$toast.success("تکمیل شده ها با موفقیت حذف شده اند")
      }
    },
    dragstart(index){
      this.draggging = index
    },
    drop(index){
      let newElement = this.todos.splice(this.draggging,1)[0]
      this.todos.splice(index,0,newElement)
    },
    changeTabHandler(tab){
      this.activeTab = tab
    }
  },
  computed:{
    ActiveTodoCount(){
      return this.todos.filter(f => f.isCompleted === false).length
    },
    filteredTodos() {
    if (this.activeTab === 'all') return this.todos;
    if (this.activeTab === 'active') return this.todos.filter(todo => !todo.isCompleted);
    if (this.activeTab === 'completed') return this.todos.filter(todo => todo.isCompleted);
    return this.todos;
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
