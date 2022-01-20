<template>
  <header class="d-flex">
    <h1>{{ title }}</h1>
    <div @mouseup="emitChangeDay" class="d-flex align-items-center daynigt__button">
      <i v-if="this.day" class="fas fa-sun"></i>
      <i v-else class="fas fa-moon"></i>
    </div>
  </header>
</template>

//++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

<script>
export default {

  name: "Header",

  data(){
      return{
          showFilter:"all",
      }
  },

  props: {
    title: String,
    day:Boolean
  },

  methods:{
    emitChangeDay(){
      this.$emit('changeDayNight');
    }
  }
  
};
</script>

//++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

<style scoped lang="scss">
    header{
        justify-content: space-between;
        h1{
            margin:.725rem .25px;
        }
    }
</style>