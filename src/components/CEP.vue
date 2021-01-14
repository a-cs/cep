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
  </div>
</template>

<script>
import api from "../services/api";

export default {
  name: "CEP",
  data() {
    return {
      cep: ""
    };
  },

  methods: {
    async getData() {
      const response = await api.get(this.cep);
      console.log(response.data);
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
