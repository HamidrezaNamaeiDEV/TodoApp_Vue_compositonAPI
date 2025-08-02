<template>
        <div class="card stat">
      <p class="corner"><span id="items-left">0</span> مورد باقی مانده</p>
      <div class="filter">
        <button id="all" class="on">همه</button>
        <button id="active" >فعال</button>
        <button id="completed">تکمیل</button>
      </div>
      <div class="corner">
        <button @click="deleteAllCompleted" id="clear-completed">حذف تکمیل شده ها</button>
      </div>
    </div>
</template>
<script>
export default{
  methods:{
    deleteAllCompleted(){
      this.$emit("deleteAllCompleted")
    }
  }
}
</script>