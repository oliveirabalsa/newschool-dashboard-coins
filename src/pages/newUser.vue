<template>
  <q-layout class="bg-mid-purple m-0 p-0" view="lHh Lpr lFf">
    <ToolBar type="back" />
    <div class="container">
      <div class="title">Cadastro de Novo Usuário</div>
      <form class="d-flex column">
        <div class="card bg-dark-purple">
          <label for="name" class="font-bold text-white font-title-field"
            >Nome do voluntário</label
          >
          <input id="name" value="" class="input" v-model="name" />
        </div>
        <div class="card  bg-dark-purple">
          <label for="email" class="font-bold text-white font-title-field"
            >E-mail do voluntário</label
          >
          <input id="email" value="" class="input" v-model="email" />
        </div>
        <div class="card  bg-dark-purple">
          <label for="coins" class="font-bold text-white font-title-field"
            >Moedas Iniciais</label
          >
          <input
            id="coins"
            placeholder="Padrão: 0"
            value="0"
            type="number"
            class="input text-white input-coins font-1-5 "
            v-model="moneyQuantity"
          />
        </div>
        <div class="card bg-dark-purple">
          <label
            for="coins"
            class="font-bold text-white font-title-field"
            style="margin-top: 10px"
            >Tipo</label
          >
          <div class="d-flex row" id="div-radio">
            <div class="col">
              <input type="radio" v-model="type" value="raiz" />

              <label for="type" class="text-white font-bold font-title-field"
                >Raíz</label
              >
            </div>
            <div class="col">
              <input type="radio" v-model="type" value="nutella" />

              <label
                for="type"
                class="text-white font-bold font-title-field radio-button"
                >Nutella</label
              >
            </div>
          </div>
        </div>
        <button
          @click.prevent="register"
          class="register-button position-absolute fixed-bottom"
        >
          CADASTRAR
        </button>
      </form>
    </div>

    <div class="alert bg-light-green text-white" v-if="successAlert">
      Cadastrado com sucesso!
    </div>

    <div class="alert bg-dark-purple text-white" v-if="errorAlert">
      Ocorreu um erro :(
    </div>

    <div class="alert bg-yellow text-black" v-if="fieldAlert">
      Campos Incompletos!
    </div>
  </q-layout>
</template>

<script>
import ToolBar from "../components/ToolBar";
import Axios from "axios";
export default {
  components: { ToolBar },
  data: () => {
    return {
      type: null,
      errorAlert: false,
      successAlert: false,
      fieldAlert: false,
      sendRequest: true,
      name: null,
      email: null,
      moneyQuantity: 0,
      type: null
    };
  },
  methods: {
    async register() {
      const payload = {
        name: this.name,
        email: this.email,
        moneyQuantity: this.moneyQuantity,
        type: this.type,
        transactions: []
      };

      if (this.name == null || this.email == null || this.type == null) {
        this.fieldAlert = true;

        setInterval(() => (this.fieldAlert = false), 3000);

        this.sendRequest = false;
      }

      if (this.moneyQuantity == 0) this.moneyQuantity = "-";

      if (this.sendRequest) {
        try {
          await Axios.post(
            "http://newschool-dashboard-coins-back.herokuapp.com/user",
            payload
          )
            .then(resp => {
              this.successAlert = true;
              setInterval(() => (this.successAlert = false), 3000);
            })
            .catch(err => {
              this.errorAlert = true;
              setInterval(() => (this.errorAlert = false), 3000);
            });
        } catch {}
      }

      //send request to server
    }
  }
};
</script>

<style scoped>
.title {
  font-weight: bolder;
  color: white;
  font-size: 1.5em;
  padding: 0px 10px;
}

.card {
  padding: 0px 10px;
  width: 100%;
  display: flex;
  flex-direction: column;
  margin-top: 5px;
}

.container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  height: 100vh;
}

.card label {
  margin: 0;
}

.card input {
  padding-top: 10px !important;
  background-color: #7a00e3;
  color: white;
}

.card input[type="radio"] {
  margin-right: 5px;
}

#div-radio {
  padding: 15px 0px;
  width: 200px;
}

.register-button {
  margin-top: 5px;
  padding: 10px 0px;
  font-weight: bolder;
  font-size: 2em;
  background-color: #04d98b;
  color: #00a16f;
  border: 0;
  width: 100%;
}

.radio-button input:checked {
  background-color: violet;
}
</style>
