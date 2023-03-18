<template>
  <div class="message_container rounded">
    <p class="alert alert-primary" role="alert">{{ msg }}</p>
  </div>
</template>

<script>
  export default {
    name: 'Message',
    props: {
      msg: String
    }
  
  }
</script>

<style scoped>
  .message_container {
    padding: 10px;
    max-width: 400px;
    max-height: 80px;
    margin: auto;
  }

</style>