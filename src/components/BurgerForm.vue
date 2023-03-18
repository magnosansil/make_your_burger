<template>
  <div id="form_group">
    <Message :msg="msg" v-show="msg"/>
    <h2 class="sub_title">Monte o seu burger:</h2>
    <div>
      <form id="burger_form" @submit="createBurger" class="rounded">
        <div class="input_container item1">
          <label class="rounded" for="nome">Nome do cliente:</label>
          <input class="form-control" type="text" id="nome" name="nome" v-model="nome" placeholder="Digite o seu nome" required>
        </div>
        <div class="input_container item2">
          <label class="rounded" for="pao">Escolha o pão:</label>
          <select name="pao" id="pao" v-model="pao" required class="form-select">
            <option value="" disabled>Selecione o seu pão</option>
            <option v-for="pao in paes" :key="pao.id" :value="pao.tipo">{{ pao.tipo }}</option>
          </select>
        </div>
        <div class="input_container item3">
          <label class="rounded" for="carne">Escolha a carne do seu Burger:</label>
          <select name="carne" id="carne" v-model="carne" required class="form-select">
            <option value="" disabled>Selecione o tipo de carne</option>
            <option v-for="carne in carnes" :key="carne.id" :value="carne.tipo">{{ carne.tipo }}</option>
          </select>
        </div>
        <div class="input_container item4" id="acompanhamentos_container">
          <label class="rounded" id="acompanhamentos_title" for="acompanhamentos">Escolha os acompanhamentos:</label>
          <div class="checkbox_container form-check" v-for="acomp in acompanhamentosData" :key="acomp.id">
            <input class="form-check-input" type="checkbox" name="acompanhamentos" v-model="acompanhamentos" :value="acomp.tipo">
            <span>{{ acomp.tipo }}</span>
          </div>
        </div>
        <div class="input_container item5">
          <input type="submit" class="submit_btn btn btn-outline-warning" value="Criar meu Burger!">
        </div>
      </form> 
    </div>
  </div>
</template>

<script>
  import Message from './Message.vue'

  export default {
    name: 'BurgerForm',
    components: {
      Message
    },
    data() {
      return {
        paes: null,
        carnes: null,
        acompanhamentosData: null,
        nome: null,
        pao: '',
        carne: '',
        acompanhamentos: [],
        msg: null
      }
    },
    methods: {
      async getIngredientes() {

        const req = await fetch("http://localhost:3000/ingredientes");
        const data = await req.json();

        this.paes = data.paes;
        this.carnes = data.carnes;
        this.acompanhamentosData = data.acompanhamentos
      },
        async createBurger(e) {
          e.preventDefault();

          const data = {
            nome: this.nome,
            carne: this.carne,
            pao: this.pao,
            acompanhamentos: Array.from(this.acompanhamentos),
            status: 'Solicitado'
          }

          const dataJson = JSON.stringify(data);

          const req = await fetch("http://localhost:3000/burgers", {
            method: 'POST',
            headers: {'Content-Type': 'application/json'},
            body: dataJson
          });

          const res = await req.json();

          this.msg = `Pedido nº ${res.id} realizado com sucesso.`

          setTimeout(() => this.msg = '', 5000);

          this.nome = '';
          this.pao = '';
          this.carne = '';
          this.acompanhamentos = [];
      }
    },
    mounted() {
      this.getIngredientes();
    }
  }
</script>

<style scoped>
  #form_group {
    margin-left: 50vw;
    padding-top: 1em;
  }

  #burger_form {
    max-width: 26vw;
    background-color: rgba(54, 54, 54, 0.5);
    margin: 0 auto;
    padding: 20px;
  }

  .sub_title {
   color: #f5f5fa;
   font-size: 49px;
   padding-bottom: 10px;
   margin: 0 auto;
  }

  .input_container {
    display: flex;
    flex-direction: column;
    margin-bottom: 20px;
  }

  label {
    font-weight: bold;
    margin-bottom: 15px;
    color: #f5f5fa;
    padding: 5px 10px;
    border-left: 4px solid #fcba03;
    height: auto;
    width: 23vw;
    background-color: rgba(252, 186, 3, 0.299) ;
  }

  input, select, .form-check-input {
    padding: 5px 8px;
    width: 23vw;
  }

  input, select {
    background-color: #f5f5fa;

  }
  .form-check span{
    margin-right: 10px;
  }

  ::placeholder{
    color: #00000054;;
  }

  #acompanhamentos_container {
    flex-direction: row;
    flex-wrap: wrap;
  }

  .checkbox_container {
    display: flex;
    align-items: flex-start;
    width: 50%;
    margin-bottom: 20px;
  }

  .checkbox_container span,
  .checkbox_container input {
    width: auto;
    color: #f5f5fa;
  }

  .checkbox_container span {
    margin-left: 8px;
  }

  .checkbox_container input {
    cursor: pointer;
  }

  .submit_btn {
    background-color: #fcba03;
    color:#222;
    font-weight: bold;
    border: 2px solid #222;
    padding: 10px;
    font-size: 20px;
    margin: 0 auto;
    cursor: pointer;
    transition: 0.3s;
    width: 100%;
  }

  .submit_btn:hover {
    background-color: #222;
    color: #fcba03;
    border-color: #fcba03;
  }

  @media (max-width: 1400px) {
    .item1 {
      grid-area: item1;
    }
    .item2 {
      grid-area: item2;
    }
    .item3 {
      grid-area: item3;
    }
    .item4 {
      grid-area: item4;
    }
    .item5 {
      grid-area: item5;
    }

    #form_group {
      margin-left: 40vw;
      padding-top: 3em;
    }

    #burger_form {
      max-width: 45vw;
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      grid-template-areas: 
      "item1 item1 item4 item4"
      "item2 item2 item4 item4"
      "item3 item3 item5 item5"
      ;
      column-gap: 40px;
      row-gap: 15px;
    }

    .input_container {
      margin-bottom: 0;
    }

    .checkbox_container {
      margin-bottom: 10px;
    }

    .submit_btn {
      height: 100%;
      font-size: 25px;
    }

    label {
      font-size: 15px;
    }

    input, select, label {
      width: 20vw;
    }

    input, select {
      padding: 3px 6px;
    }
  }

  @media (max-width: 1284px) {
    #burger_form {
      max-width: 50vw;
    }

    input, select, label {
      width: 22vw;
    }
    .submit_btn {
      padding: 5px;
    }
  }

  @media (max-width: 1104px){
    #form_group {
      margin-left: 38vw;
    }

    #burger_form {
      max-width: 52vw;
    }

    input, select, label {
      width: 24vw;
    }
    .submit_btn {
      font-size: 20px;
    }
  }

  @media (max-width: 1007px) {
    #form_group {
      padding-top: 2em;
      margin-left: auto;
      margin-right: auto;
    }

    #burger_form {
      display: block;
      max-width: 50%;
    }

    label {
      width: 100%;
      font-size: 1em;
    }

    input, select {
      padding: 5px 8px;
      width: 100%;
      margin-bottom: 15px;
    }
    .submit_btn {
      font-size: 25px;
    }
  }

  @media (max-width: 754px) {
    #burger_form {
      max-width: 70%;
    }
  }

  @media (max-width: 522px) {
    #burger_form {
      max-width: 95%;
    }

    .sub_title {
      font-size: 30px;
    }
  }

  @media (max-width: 456px) {
    label, input, select, 
    .form-check span {
      font-size: 0.8rem;
    }
    .submit_btn {
      font-size: 20px;
    }
  }

</style>