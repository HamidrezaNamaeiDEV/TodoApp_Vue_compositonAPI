<template>
  <app-header></app-header>
  <main>
   <add-todo @AddnewTodo="AddToDoItem"></add-todo>
    <ul class="todos">
     <todo-item v-for="(item,i) in filteredTodos" :key="item.id" :todo="item" @ondgiteleted="deleteTodo" @changeStatus="changeTodoStatus" @dragover.prevent @dragstart="dragstart(i)" @drop="drop(i)"></todo-item>       
    </ul>
    <app-filter @deleteAllCompleted = "deleteAllCompleted" :activeCount="ActiveTodoCount" @changeTab ="changeTabHandler" :activeTab="activeTab"></app-filter>
  </main>
    <app-footer></app-footer>
</template>

<script setup>
import AppHeader from './components/AppHeader.vue';
import AppFooter from './components/AppFooter.vue';
import AddTodo from './components/AddTodo.vue';
import TodoItem from './components/ToDo.vue';
import AppFilter from './components/AppFilter.vue';
import {ref, computed} from 'vue';
import {useToast} from 'vue-toast-notification';
import 'vue-toast-notification/dist/theme-default.css';
    

    const $toast = useToast();
    console.log($toast)
    let todos = ref([])
    const draggging = ref(-1)
    const activeTab = ref("all")

    function AddToDoItem(title){
      if(!title){
      $toast.error("لطفا متن تودو را پر کنید")
      }
      else{
      const id = Math.random().toString(16).slice(2)
      const todo = {id ,title , isCompleted : false}
      todos.value.push(todo)
      $toast.success("تودو جدید اضافه شد")
      }

    }
    function deleteTodo(id){
      const todo = todos.value.find(todo=>todo.id == id)
      todos.value = todos.value.filter(todo=>todo.id !== id)
      $toast.error(`${todo.title} حذف شد`)
    }
    function changeTodoStatus(id,newStatus){
      let newTodos = [...todos.value];
      let selectedTodo = newTodos.find(item=>item.id === id)
      selectedTodo.isCompleted = newStatus
      todos.value = newTodos;
    }
    function deleteAllCompleted(){
      if(confirm("ایا ا پاک کردن تمامی تکمیل شده ها مطمئن هستید؟")){
      let newTodos = [...todos.value];
      newTodos = newTodos.filter(f =>f.isCompleted === false);
       todos.value = newTodos
       $toast.success("تکمیل شده ها با موفقیت حذف شده اند")
      }
    }
    function dragstart(index){
      draggging.value = index
    }
    function drop(index){
      let newElement = todos.value.splice(draggging.value,1)[0]
      todos.value.splice(index,0,newElement)
    }
    function changeTabHandler(tab){
      activeTab.value = tab
    }
  
    const ActiveTodoCount = computed(()=>{
      return todos.value.filter(f => f.isCompleted === false).length
    })
    const filteredTodos = computed(()=> {
    if (activeTab.value === 'all') return todos.value;
    if (activeTab.value === 'active') return todos.value.filter(todo => !todo.isCompleted);
    if (activeTab.value === 'completed') return todos.value.filter(todo => todo.isCompleted);
    return todos.value;
  })

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
