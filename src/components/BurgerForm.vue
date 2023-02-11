<template>
  <div>
    <Message :msg="msg" v-show="msg"/>
    <div>
      <form action="" id="form-burguer" @submit="createBurger">
        <div class="input-container">
          <label for="name">Nome do cliente:</label>
          <input 
            type="text" 
            name="name" 
            id="name" 
            v-model="nome" 
            placeholder="Digite o sue nome"
          >
        </div>
        <div class="input-container">
          <label for="bread">Escolha o pão:</label>
          <select name="bread" id="pao" v-model="pao">
            <option value="SelecioneSeuPao">Selecione o seu pão</option>
            <option v-for="opcoes in paes" 
              :key="opcoes.id" 
              :value="opcoes.tipo"
            >
              {{ opcoes.tipo }}
            </option>
          </select>
        </div>
        <div class="input-container">
          <label for="meat">Escolha sua carne:</label>
          <select name="meat" id="carne" v-model="carne">
            <option value="SelecioneSuaCarne">Selecione a sua carne</option>
            <option v-for="opcoes in carnes" 
              :key="opcoes.id"  
              :value="opcoes.tipo">
              {{ opcoes.tipo }}
            </option>
          </select>
        </div>
        <div id="opcionais-container" class="input-container">
          <label class="optionals-title" for="'optionals'">Selecione os opcionais:</label>
          <div v-for="opcoes in opcionais" :key="opcoes.id" class="checkbox-container">
            <input 
              type="checkbox" 
              name="optionals"
              v-model="opcionaisData"
              :value="opcoes.tipo"
            >
            <span>{{ opcoes.tipo }}</span>
          </div>
        </div>
        <div class="input-container">
          <input type="submit" value="Criar meu burguer" class="btn-submit">
        </div>
      </form>
    </div>
  </div>
</template>
<script>
  import axios from 'axios';
  import Message from './Message.vue';

  export default {
    name: 'BurgerForm',
    components:{
      Message,
    },
    data() {
      return{
        nome: null,
        pao: 'SelecioneSeuPao',
        carne: 'SelecioneSuaCarne',
        opcionaisData: [],
        nomes: null,
        paes: null,
        carnes: null,
        opcionais: [],
        status: null,
        msg: null
      }
    },
    methods: {
      async getIngredients() {
        axios.get('https://my-json-server.typicode.com/Luiz-Farias-dev/letburger-json-server/ingredientes')
        .then(
          (response)=>{
            this.carnes = response.data.carnes;
            this.opcionais = response.data.opcionais;
            this.paes = response.data.paes;
          }
        )
        .catch((err) => {console.log(`Error mensagem: ${err}`)})
      },
      async createBurger(e) {
        e.preventDefault();
        const data = {
          nome: this.nome,
          carne: this.carne,
          pao: this.pao,
          opcionaisData: Array.from(this.opcionaisData),
          status: 'Solicitado'
        }
        axios.post('https://my-json-server.typicode.com/Luiz-Farias-dev/letburger-json-server/burgers', data)
        .then((response) => {
          console.log(response);
          this.msg = `Pedino Nº${response.data.id} realizado com sucesso`;
          setTimeout(() => {
            this.msg = null;
          }, 2000)
        })
        
        //colocar uma msg no sistema
        this.msg = "Pedido realizado com sucesso"

        //limpar msg
        
        // Limpar campos
        this.nome = '';
        this.carne = 'SelecioneSuaCarne';
        this.pao = 'SelecioneSeuPao';
        this.opcionaisData = [];
        this.status = '';
      }
    },
    mounted() {
      this.getIngredients();
    }
}
</script>
<style scoped>
  #form-burguer {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    max-width: 400px;
    margin: 0 auto;
  }
  .input-container {
    display: flex;
    flex-direction: column;
    margin-bottom: 20px;
  }
  label {
    font-weight: bold;
    margin-bottom: 15px;
    color: #222;
    padding: 5px 10px;
    border-left: 4px solid #FCBA03;
  }
  input, select {
    padding: 5px 10px;
    width: 300px;
  }
  #opcionais-container {
    flex-direction: row;
    flex-wrap: wrap;
    width: 300px;
  } 
  .optionals-title {
    width: 100%;
  }
  
  .checkbox-container {
    display: flex;
    align-items: flex-start;
    width: 50%;
    margin-bottom: 20px;
  }
  .checkbox-container span,
  .checkbox-container input {
    width: auto;
  }
  .checkbox-container span {
    margin-left: 6px;
    font-weight: bold;
  }
  .btn-submit {
    background-color: #222;
    color: #FCBA03;
    font-weight: bold;
    border: 2px solid #222;
    padding: 20px;
    font-size: 16px;
    margin: 0 auto;
    cursor: pointer;
    transition: .5s;
  }
  .btn-submit:hover {
    background-color: transparent;
    color: #222;
  }
</style>