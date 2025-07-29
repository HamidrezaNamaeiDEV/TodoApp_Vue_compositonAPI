<template>
  <app-header></app-header>
  <main>
   <add-todo></add-todo>
    <ul class="todos">
     <todo-item></todo-item>       
     <todo-item></todo-item>       
     <todo-item></todo-item>       
    </ul>
    <app-filter></app-filter>
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
