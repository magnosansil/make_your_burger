<template>
  <div id="burger_table">
    <Message :msg="msg" v-show="msg"/>
    <div class="content">
      <div id="burger_table_heading">
        <div class="order_id">#:</div>
        <div class="name">Cliente:</div>
        <div>Pão:</div>
        <div>Carne:</div>
        <div class="company">Adicionais:</div>
        <div>Ações:</div>
      </div>
      <div id="burger_table_rows">
        <div class="burger_table_row" v-for="burger in burgers" :key="burger.id">
          <div class="order_number">{{ burger.id }}</div>
          <div class="name">{{ burger.nome }}</div>
          <div class="name">{{ burger.pao }}</div>
          <div>{{ burger.carne }}</div>
          <div class="company">
            <ul>
              <li v-for="(acompanhamento, index) in burger.acompanhamentos" :key="index">{{ acompanhamento }}</li>
            </ul>
          </div>
          <div class="buttons">
            <select name="status" class="status rounded" @change="updateBurger($event, burger.id)">
              <option value="" disabled>Selecione</option>
              <option v-for="s in status" :key="s.id" :value="s.tipo" :selected="burger.status === s.tipo">{{ s.tipo }}</option>
            </select>
            <button class="delete_btn rounded btn btn-danger" @click="deleteBurger(burger.id)">Cancelar</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import Message from './Message.vue';

  export default {
    name: 'Dashboard', 
    data() {
      return {
        burgers: null,
        burger_id: null,
        status: [],
        msg: null
      }
    },
    methods: {
      async getPedidos() {
        const req = await fetch("http://localhost:3000/burgers");

        const data = await req.json();

        this.burgers = data;

        this.getStatus();
      },
      async getStatus() {

        const req = await fetch("http://localhost:3000/status");

        const data = await req.json();

        this.status = data;
      },
      async deleteBurger(id) {
        const cancelOrder = prompt ('Deseja cancelar o pedido? (S/N)') 
        if (cancelOrder.toUpperCase() === 'S' || cancelOrder.toUpperCase() === 'SIM') {
          const req = await fetch(`http://localhost:3000/burgers/${id}`, {
          method: 'DELETE'
        });

        const res = await req.json();

        
        this.msg = `Pedido nº ${id} removido com sucesso.`

        setTimeout(() => this.msg = '', 5000);

        this.getPedidos();
        }
        
      },

      async updateBurger(event, id) {

        const option = event.target.value;

        const dataJson = JSON.stringify({ status: option });

        const req = await fetch(`http://localhost:3000/burgers/${id}`, {
          method: 'PATCH',
          headers: { "Content-Type": "application/json"},
          body: dataJson
        });

        const res = await req.json();
      }
    },
    mounted() {
      this.getPedidos();
    },
    components: {
      Message
    }
  }
</script>

<style scoped>
  .content {
    width: 86vw;
    margin: 0 auto;
  }

  #burger_table_heading,
  #burger_table_rows,
  .burger_table_row {
    display: flex;
    flex-wrap: wrap;
  }

  #burger_table_heading {
    font-weight: bold;
    padding: 12px;
    border-bottom: 3px solid #333;
  }

  #burger_table_heading div,
  .burger_table_row div {
    width: 18%;
  }

  #burger_table_heading div {
    overflow: hidden;
  }

  .burger_table_row {
    width: 100%;
    padding: 12px;
    border-bottom: 1px solid #ccc;
  }

  #burger_table_heading .order_id,
  .burger_table_row .order_number {
    width: 5%;
  }

  .name {
    overflow: hidden;
    max-width: 20%;
    margin-right: 15px;
  }

  .company {
    margin-left: -100px;
  }

  .buttons {
    display: flex;
  }
  
  select {
    padding: 16px 6px;
    margin-right: 12px; 
    margin-bottom: 12px;
    height: 65px;
  }

  .delete_btn {
    color: #f5f5fa;
    border: 1px solid #222;
    padding: 12px;
    font-size: 16px;
    height: 65px;
  }
</style>