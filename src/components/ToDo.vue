<template>
      <li class="card" draggable="true">
        <div class="cb-container">
          <input type="checkbox" :checked="todo.isCompleted ? true : null" class="cb-input" @click="changeStatus"/>
          <span class="check"></span>
        </div>
        <p class="item" >
          <del v-if="todo.isCompleted">{{todo.title}}</del>
          <span v-else>{{todo.title}}</span>
        </p>
        <button class="clear" @click=deleteTodo>
          <img src="../../public/assets/images/icon-cross.svg" alt="Clear it" />
        </button>
      </li>

</template>
<script setup>
import {defineProps , defineEmits} from "vue"
  const props = defineProps({
    todo : Object
  })
  const emits = defineEmits(['onDeleted','changeStatus'])
  function deleteTodo(){
      if (confirm("ایا از حذف مطمئن اید؟")) {
        emits("onDeleted",props.todo.id)
      }
    }
  function changeStatus(){
      emits("changeStatus",props.todo.id,!props.todo.isCompleted)
  }
</script>