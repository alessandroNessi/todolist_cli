<template>
  <footer class="d-flex flex-column">
      <h5 class="intestation">credits:</h5>
      <a class="credits" href='https://www.freepik.com/vectors/background'>Background vector created by BiZkettE1 - www.freepik.com</a>
  </footer>
</template>

<script>
export default {
    name:"Footer",
}
</script>

<style scoped lang="scss">
    .intestation{
        margin-top: 1rem;
    }
    .credits{
        text-decoration: none;
        color: #6666ff;
        font-size: 00.5rem;
        // margin:0px;
    }
    @media screen and (max-height: 600px) {
        .intestation{
            margin-top: 0.3rem;
        }
    }
</style>