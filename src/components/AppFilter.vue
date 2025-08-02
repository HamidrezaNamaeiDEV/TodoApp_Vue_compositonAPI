<template>
        <div class="card stat">
      <p class="corner"><span id="items-left">{{activeCount}}</span> مورد باقی مانده</p>
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
  props:{
    activeCount:{
      type : Number,
      required: true
    }
  },
  methods:{
    deleteAllCompleted(){
      this.$emit("deleteAllCompleted")
    }
  }
}
</script>