<template>
<main>
  <div class="app">
    <div id="title">
    <h1>CEPV2 API - Brasil</h1>
      <input id="input" type="text" placeholder="Informe um CEP" v-model="query">
      <input type="button" value="Pesquisar" id="btn-pesquisar" v-on:click="fetchCep" >
    </div>

    <div id="result">
      <h1 id="status">{{ status }}</h1>
      <h2>CEP: {{ api.cep }}</h2>
      <h2>Estado: {{ api.state }}</h2>
      <h2>Cidade: {{api.city }}</h2>
    </div>

  </div>
  </main>
</template>

<script>
    import axios from "axios";
    export default {
    name: 'app',
    data () {
      return {
        url_base: 'https://brasilapi.com.br/api/cep/v2',
        query: '',
        status: '',
        api: {}
      }
    },
    methods: {
        async fetchCep () {
            await axios.get(`${this.url_base}/${this.query}`).then(res => { 
              if(res.status == 200){
                this.status = '';
                return res.data;
              }
              }).then(res => (this.api = res)).catch(error => {
                this.status = 'CEP Não encontrado';
                this.api = '';
              });
            }
        },
      }
    
</script>

<style>
.app {
  display: flex;
  flex-direction: column;
  align-items: center;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

#result {
  margin-top: 40px;
  font-style: italic;
}

#status {
  font-style: italic;
  color: red;
  margin-bottom: 50px;
}

#input, #btn-pesquisar {
  padding: 0.25em;
  text-align: center;
  margin-left: 0.1em;
  font-style: italic;
  font-size: 16px;
  outline: 0;
}

#input:hover {
  border: 0.13em outset rgb(71, 71, 73);
}


</style>
