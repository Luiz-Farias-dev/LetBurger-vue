<template>
  <div id="burger-table">
    <div>
      <Message :msg="msg" v-show="msg"/>
      <div class="burger-table-heading">
        <div  class="order-id">#:</div>
        <div>Cliente:</div>
        <div>Pão:</div>
        <div>Carne:</div>
        <div>Opcionais:</div>
        <div>Ações:</div>
      </div>
    </div>
    <div class="burger-table-rows">
      <div v-for="item in burgers" :key="item.id" class="burger-table-row">
        <div class="order-number">{{ item.id }}</div>
        <div>{{ item.nome }}</div>
        <div>{{ item.pao }}</div>
        <div>{{ item.carne }}</div>
        <div>
          <ul>
            <li v-for="(opcao, index) in item.opcionaisData" :key='index'>
             {{ opcao }}
            </li>
          </ul>
        </div>
        <div>
          <select name="status" class="status" @change="updateStatus($event, item.id)">
            <option value="">Selecione</option>
            <option v-for="i in status" :key='i.id' :value="item.tipo" :selected="item.status == i.tipo">{{ i.tipo }}</option>
          </select>
          <button class="delete-btn" @click="deleteBurger(item.id)">Cancelar</button>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
  import axios from 'axios';
  import Message from './Message.vue';

  export default {
    name: 'Dashboard',
    components: {
      Message,
    },
    data() {
      return {
        burgers: null,
        burger_id: null,
        status: [],
        msg: null,
      }
    },
    methods: {
      async getBurgers() {
        axios.get('https://my-json-server.typicode.com/Luiz-Farias-dev/letburger-json-server/burgers')
        .then((res) => {
          this.burgers = res.data;
          console.log(res.data);
          console.log(res.data.opcionaisData);
        })
        .catch(err => {
          console.log(err);
        })
        this.getStatus();
      },
      async getStatus() {
        axios.get('https://my-json-server.typicode.com/Luiz-Farias-dev/letburger-json-server/status')
        .then(res =>{
          this.status = res.data;
          console.log(res.data);
          console.log(res.data.tipo);
        })
      },
      deleteBurger(data) {
        axios.delete(`https://my-json-server.typicode.com/Luiz-Farias-dev/letburger-json-server/burgers/${data}`)
        this.getBurgers();
        this.msg=`Pedido Nº${data} foi deletado com sucesso`;
        setTimeout(() => {
          this.msg = null;
        }, 2000);
      },
      updateStatus(event, id) {
        const option = event.target.value;
        axios.patch(`https://my-json-server.typicode.com/Luiz-Farias-dev/letburger-json-server/burgers/${id}`, {
          status: option,
        })
        this.msg = `Status do pedido Nº${id} alterado com sucesso`;
        setTimeout(() => {
          this.msg = null;
        }, 2000);
      }
    },
    mounted() {
      this.getBurgers();
    },
  }
</script>
<style scoped>
  #burger-table {
    max-width: 1200px;
    margin: 0 auto;
  }

  .burger-table-heading,
  .burger-table-rows,
  .burger-table-row{
    display: flex;
    flex-wrap: wrap;
  }

  .burger-table-heading {
    font-weight: bold;
    padding: 12px;
    border-bottom: 3px solid #333;
  }

  .burger-table-heading div,
  .burger-table-row div {
    width: 19%;
  }

  .burger-table-row {
    width: 100%;
    padding: 12px;
    border-bottom: 1px solid #ccc;
  }

  .burger-table-heading .order-id,
  .burger-table-row .order-number {
    width: 5%;
  }

  select {
    padding: 12px 6px;
    margin-right: 12px;
  }

  .delete-btn {
    background-color: #222;
    color: #FCBA03;
    font-weight: bold;
    border: 2px solid #222;
    padding: 10px;
    font-size: 16px;
    margin: 0 auto;
    cursor: pointer;
    transition: .5s;
  }

  .delete-btn:hover {
    background-color: transparent;
    color: #222;
  }
</style>