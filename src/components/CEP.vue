<template>
  <div class="CEP">
    <h2>Olá qual CEP você gostaria de consultar?</h2>
    <form>
      <input
        type="text"
        ref="input"
        v-model="cep"
        placeholder="Digite o CEP"
        @keydown.enter.prevent="getData()"
        @input="preventInvalidInput"
        maxlength="9"
        v-mask="'#####-###'"
      />
      <input type="submit" @click.prevent="getData()" value="Consultar" />
    </form>
    <div class="error" v-if="error">
      <p>
        O CEP <b>{{ error }}</b> não foi encontrado, por favor tente novamente.
      </p>
    </div>
    <div class="infos" v-if="infos">
      <div class="info-line">
        <div class="info-title">
          <p><b>CEP: </b></p>
        </div>
        <div class="info-blank" />
        <div class="info-description">
          <p>
            {{ infos.cep }}
          </p>
        </div>
      </div>
      <div class="info-line">
        <div class="info-title">
          <p><b>Logradouro: </b></p>
        </div>
        <div class="info-blank" />
        <div class="info-description">
          <p>
            {{ infos.logradouro }}
          </p>
        </div>
      </div>
      <div class="info-line">
        <div class="info-title">
          <p><b>Complemento: </b></p>
        </div>
        <div class="info-blank" />
        <div class="info-description">
          <p>
            {{ infos.complemento }}
          </p>
        </div>
      </div>
      <div class="info-line">
        <div class="info-title">
          <p><b>Bairro: </b></p>
        </div>
        <div class="info-blank" />
        <div class="info-description">
          <p>
            {{ infos.bairro }}
          </p>
        </div>
      </div>
      <div class="info-line">
        <div class="info-title">
          <p><b>Cidade: </b></p>
        </div>
        <div class="info-blank" />
        <div class="info-description">
          <p>
            {{ infos.cidade }}
          </p>
        </div>
      </div>
      <div class="info-line">
        <div class="info-title">
          <b>Estado: </b>
        </div>
        <div class="info-blank" />
        <div class="info-description">
          <p>
            {{ infos.estado }}
          </p>
        </div>
      </div>
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
        this.error = null;
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
.CEP {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;

  h2 {
    font-size: 35px;
    padding: 10px 0;
  }

  form {
    width: 100%;
    display: flex;
    flex-direction: column;

    input {
      height: 60px;
      font-size: 35px;
      margin: 2px 0;
      padding: 2px 4px;
      color: #1a73e8;

      &:focus,
      &:active {
        border: 4px solid #03aefd;
      }
    }
    input[type="submit"] {
      background: #1a73e8;
      height: 60px;
      color: white;
      margin: 8px 0 10px;

      &:hover {
        background: #03aefd;
      }
    }
  }

  .infos {
    width: 100%;
  }

  .info-line {
    display: flex;
    align-items: center;
    font-size: 25px;
    border: 1px solid lightslategrey;
    /* margin: 4px; */
    padding: 4px;

    b {
      color: #03aefd;
    }
  }
  .error {
    margin: 25px;
    font-size: 25px;
    p {
      border: none;
    }
    b {
      color: #fc5426;
    }
  }

  .info-blank {
    flex-grow: 1;
  }

  .info-description {
    text-align: end;
  }
}

@media (min-width: 700px) {
  .CEP {
    .error {
      font-size: 35px;
    }

    .info-line {
      font-size: 35px;
    }
  }
}
</style>
