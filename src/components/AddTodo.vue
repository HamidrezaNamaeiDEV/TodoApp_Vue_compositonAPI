<template>
        <div class="card add">
      <div class="cb-container">
        <button id="add-btn" @click="AddTodo">+</button>
      </div>
      <div class="txt-container">
        <label for="addt">افزودن </label>
        <input v-model="title" type="text" class="txt-input" placeholder="افزودن وظیفه جدید..." spellcheck="false" autocomplete="off" 
          id="addt" dir="rtl" @keypress.enter="AddTodo"/>
      </div>
    </div>
</template>
<script>
export default{
    data(){
      return{
        title : "",
      };
    },
    methods:{
      AddTodo(){
        this.$emit("AddnewTodo",this.title)
        this.title = "";
      }
    }
}
</script>