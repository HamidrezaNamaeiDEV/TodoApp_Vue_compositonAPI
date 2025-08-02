<template>
      <header class="card">
    <h1>لیست وظایف </h1>
    
    <button id="theme-switcher" @click="changeTheme">
      <img v-if="defaultTheme == 'dark'" :src= this.sunImage alt="Change color theme" />
      <img v-else :src= this.moonImage alt="Change color theme" />
    </button>
  </header>
</template>
<script>
export default{
    data() {
      return {
        sunImage : "assets/images/icon-sun.svg",
        moonImage : "assets/images/icon-moon.svg",
        defaultTheme : 'dark',
      }
    },
    methods:{
      changeTheme(){
        if (this.defaultTheme == "dark") {
          this.defaultTheme = "light"
          document.querySelector('body').classList.add('light')
        }
        else{
          this.defaultTheme = "dark"
          document.querySelector('body').classList.remove('light')
        }
      }
    }
}
</script>