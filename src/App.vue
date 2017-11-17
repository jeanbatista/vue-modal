<template>
  <div id="app">
    <button id="show-modal" @click="showModal = true">Show Modal</button>
    <!-- use the modal component, pass in the prop -->
    <modal v-if="showModal" @close="showModal = false">
      <h3 slot="header">Cadastro</h3>
    
      <div slot="body">
        <label>Nome:</label><br />
        <input type="text" v-model="pessoa.nome"  @keyup.enter="trigger"/>
        <br />
        <label>Sobrenome:</label><br />
        <input type="text" v-model="pessoa.sobrenome" @keyup.enter="trigger" /> 
        <br />
        <label>Idade:</label><br />
        <input type="number" v-model="pessoa.idade" @keyup.enter="trigger" />             
      </div>

      <div slot="footer">
        <button class="btn-container" @click="okClick" ref="sendReply">OK</button>
        <button class="btn-container" @click="showModal = false">Cancelar</button>
      </div>
    </modal>
    <br>

    <table border="1">
      <tr>
        <td><br>Nome</b></td>
        <td><br>Sobrenome</b></td>
        <td><br>Idade</b></td>
      </tr>
      <tr v-for="item in listaPessoas">
        <td>{{ item.nome }}</td>
        <td>{{ item.sobrenome }}</td>
        <td>{{ item.idade }}</td>
      </tr>
    </table>
  </div>
</template>

<script>
import modal from './components/modalCommon'

export default {
  name: 'app',
  data() {
    return {
      showModal: false,
      pessoa: {
        nome: null,
        sobrenome: null,
        idade: null
      },
      listaPessoas: []
    } 
  },

  components: {
    modal
  },

  methods: {
    okClick: function() {
      let resource = { nome: "", sobrenome: "", idade: "" };
      resource.nome = this.pessoa.nome;
      resource.sobrenome = this.pessoa.sobrenome;
      resource.idade = this.pessoa.idade;

      this.listaPessoas.push(resource);
      alert("Pessoa salva com sucesso");
      this.formClear();

      this.showModal = false;
    },

    formClear: function() {
      this.pessoa.nome = null,
      this.pessoa.sobrenome = null;
      this.pessoa.idade = null;
    },

    trigger () {
    	this.$refs.sendReply.click()
    }
  }
}
</script>

<style>
  input {
    width: 100%
  }

  .btn-container {
    width: 20%;
  }
</style>
