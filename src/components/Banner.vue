<template>
  <div id="main_banner" class="container-fluid">
    <BurgerForm/>
  </div>
</template>

<script>
  import BurgerForm from './BurgerForm.vue';

  export default {
    name: 'Banner',
    components: {
      BurgerForm
    }
  }
</script>

<style scoped>
  #main_banner {
    background-image: url('../../public/img/burger.png');
    background-position: 0 -250px;
    background-size: cover;
    background-repeat: no-repeat;
    min-height: 90vh;
    padding-bottom: 4vh;
  }

 

  @media (max-width: 1763px) {
    #main_banner { 
      background-position-y: -210px;
    }
  }

  @media (max-width: 1602px) {
    #main_banner { 
      background-position-y: -150px;
    }
  }

  @media (max-width: 1500px) {
    #main_banner { 
      background-position-y: -135px;
    }
  }

  @media (max-width: 1304px) {
    #main_banner {
      background-size: 120%;
      background-position: center -155px;
    }
  }

  @media (max-width: 1104px) {
    #main_banner {
      background-size: 130%;
    }
  }

  @media (max-width: 1007px) {
    #main_banner {
      background-image: url('../../public/img/background_2.png');
      background-position-y: center;
    }
  }
  
  @media (max-width: 781px) {
    #main_banner {
      background-size: 200%;
    }
  }

   @media (max-width: 502px) {
    #main_banner {
      background-size: 300%;
    }
  }

  @media (max-width: 342px) {
    #main_banner {
      background-size: 400%;
    }
  } 
</style>