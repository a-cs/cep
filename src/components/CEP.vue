<template>
  <div class="CEP">
    <h1>Olá qual CEP você gostaria de saber mais informações?</h1>
    <input
      type="text"
      ref="input"
      v-model="cep"
      placeholder="Digite o CEP"
      v-on:keyup.enter="getData()"
      maxlength="9"
    />
    <button type="submit" @click="getData()">Procurar</button>
    <div v-if="error">
      <p>
        O CEP <b>{{ error }}</b> não foi encontrado, tente novamente.
      </p>
    </div>
    <div v-if="infos">
      <p><b>Logradouro: </b> {{ infos.logradouro }}</p>
      <p><b> Complemento: </b> {{ infos.complemento }}</p>
      <p><b> Bairro: </b> {{ infos.bairro }}</p>
      <p><b>Cidade: </b> {{ infos.cidade }}</p>
      <p><b> Estado: </b> {{ infos.estado_info.nome }} ({{ infos.estado }})</p>
    </div>
  </div>
</template>

<script>
import api from "../services/api";

export default {
  name: "CEP",
  data() {
    return {
      cep: "",
      infos: null,
      error: null
    };
  },

  watch: {
    cep() {
      this.cep = this.cep
        .replace(/[^0-9]/g, "")
        .replace(/^(\d{5})(\d{3})?/g, "$1-$2");
    }
  },

  methods: {
    async getData() {
      try {
        const response = await api.get(this.cep);
        console.log(response);
        this.infos = response.data;
        this.cep = "";
      } catch (err) {
        this.error = this.cep;
        this.infos = null;
        this.cep = "";
      }
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
/* h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
} */
</style>
