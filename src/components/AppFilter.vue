<template>
        <div class="card stat">
      <p class="corner"><span id="items-left">{{activeCount}}</span> مورد باقی مانده</p>
      <div class="filter">
        <button id="all" :class="{on : activeTab == 'all'}" @click="changeTab('all')">همه</button>
        <button id="active" :class="{on : activeTab == 'active'}" @click="changeTab('active')">فعال</button>
        <button id="completed" :class="{on : activeTab == 'completed'}" @click="changeTab('completed')">تکمیل</button>
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
    },
    activeTab:{
      type : String,
      required:true
    }
  },
  methods:{
    deleteAllCompleted(){
      this.$emit("deleteAllCompleted")
    },
    changeTab(tab){
      this.$emit("changeTab",tab)      
    }
  }
}
</script>