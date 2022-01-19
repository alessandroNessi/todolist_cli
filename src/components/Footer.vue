<template>
  <footer class="d-flex flex-column">
      <p class="intestation">credits:</p>
      <a class="credits" href='https://www.freepik.com/vectors/background'>Background vector created by BiZkettE1 - www.freepik.com</a>
  </footer>
</template>

<script>
export default {
    name:"Footer",
}
</script>

<style scoped lang="scss">
    footer{
        padding: .4rem;
    }
    .intestation{
        padding-top: 0.4rem;
        border-top: 1px solid var(--grey-400);
    }
    .credits{
        text-decoration: none;
        color: var(--purple-500);
        font-size: .5rem;
    }
</style>