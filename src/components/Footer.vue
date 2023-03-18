<template>
  <footer id="footer">
    <p class="text-center">Magno Silva &bull; Make Your Burger &copy; 2023</p>
  </footer>
</template>

<script>
  export default {
    name: 'Footer'
  }
</script>

<style scoped>
  #footer {
    height: 200px;
    background-color: #222;
    border-top: 4px solid;
    border-image: linear-gradient(to left, #f82410, #4d0000);
    border-image-slice: 1;
    color: #fcba03;
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100%;
    padding: 10px;
  }
</style>