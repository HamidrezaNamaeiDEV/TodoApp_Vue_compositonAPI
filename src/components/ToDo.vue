<template>
      <li class="card" draggable="true">
        <div class="cb-container">
          <input type="checkbox" :checked="todo.isCompleted ? true : null" class="cb-input" @click="changeStatus"/>
          <span class="check"></span>
        </div>
        <p class="item">{{todo.title}}</p>
        <button class="clear" @click=deleteTodo>
          <img src="../../public/assets/images/icon-cross.svg" alt="Clear it" />
        </button>
      </li>

</template>
<script>
export default {
  props:{
    todo:Object
  },
  methods:{
    deleteTodo(){
      if (confirm("ایا از حذف مطمئن اید؟")) {
        this.$emit("Deleted",this.todo.id)
      }
    },
    changeStatus(){
      this.$emit("changeStatus",this.todo.id,!this.todo.isCompleted)
    }
  }
}
</script>