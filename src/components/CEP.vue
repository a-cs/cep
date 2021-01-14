<template>
  <div class="CEP">
    <h1>Olá qual CEP você gostaria de saber mais informações?</h1>
    <input
      type="text"
      ref="input"
      v-model="cep"
      placeholder="Digite o CEP"
      v-on:keyup.enter="getData()"
    />
    <button type="submit" @click="getData()">Procurar</button>

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
      infos: null
    };
  },

  methods: {
    async getData() {
      const response = await api.get(this.cep);
      console.log(response.data);
      this.infos = response.data;
      this.cep = "";
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
