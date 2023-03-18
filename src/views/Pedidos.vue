<template>
  <div class="main-container" id="pedidos">
    <h2 class="sub_title">Gerenciar Pedidos</h2>
    <Dashboard/>
  </div>
</template>

<script>
  import Dashboard from '../components/Dashboard.vue';

  export default {
    name: 'Pedidos',
    components: {
      Dashboard
    }
  }
</script>

<style scoped>
  #pedidos {
    min-height: 80vh;
    background-color: #f5f5fa;
  }
  .sub_title {
    padding-top: 20px;
  }
</style>

