<template>
        <div class="card stat">
      <p class="corner"><span id="items-left">{{activeCount}}</span> مورد باقی مانده</p>
      <div class="filter">
        <button id="all" :class="{on : props.activeTab == 'all'}" @click="changeTab('all')">همه</button>
        <button id="active" :class="{on : props.activeTab == 'active'}" @click="changeTab('active')">فعال</button>
        <button id="completed" :class="{on : props.activeTab == 'completed'}" @click="changeTab('completed')">تکمیل</button>
      </div>
      <div class="corner">
        <button @click="deleteAllCompleted" id="clear-completed">حذف تکمیل شده ها</button>
      </div>
    </div>
</template>
<script setup>
import {defineEmits,defineProps} from 'vue';
  const emits = defineEmits(["deleteAllCompleted","changeTab"])
  const props = defineProps({
    activeCount :{
      type : Number,
      required: true
    },
    activeTab:{
      type : String,
      required:true
    }
  })

    function deleteAllCompleted(){
      emits("deleteAllCompleted")
    }
    function changeTab(tab){
      emits("changeTab",tab)      
    }

</script>