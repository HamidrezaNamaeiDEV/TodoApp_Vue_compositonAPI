<template>
      <li class="card" draggable="true">
        <div class="cb-container">
          <input type="checkbox" :checked="todo.isCompleted ? true : null" class="cb-input" />
          <span class="check"></span>
        </div>
        <p class="item">{{todo.title}}</p>
        <button class="clear">
          <img src="../../public/assets/images/icon-cross.svg" alt="Clear it" />
        </button>
      </li>

</template>
<script>
export default {
  props:{
    todo:Object
  }
}
</script>