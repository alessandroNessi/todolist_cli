<template>
  <header class="d-flex">
    <h1>{{ title }}</h1>
  </header>
</template>

<script>
export default {
  name: "Header",
  props: {
    title: String,
  },
};
</script>

<style scoped lang="scss">
    header{
        justify-content: space-between;
        h1{
            margin:.725rem .25px;
        }
    }
</style>