<template>
  <q-layout class="bg-mid-purple" view="lHh Lpr lFf">
    <ToolBar type="back" />
    <!-- fix menu latter -->
    <div class="container">
      <div class="title">Cadastro de Novo Usuário</div>
      <form class="d-flex column">
        <div class="card bg-dark-purple">
          <label for="name" class="font-bold text-white font-title-field"
            >Nome do voluntário</label
          >
          <input id="name" value="" class="input" />
        </div>
        <div class="card  bg-dark-purple">
          <label for="email" class="font-bold text-white font-title-field"
            >E-mail do voluntário</label
          >
          <input id="email" value="" class="input" />
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
          />
        </div>
        <div class="card bg-dark-purple">
          <label for="coins" class="font-bold text-white font-title-field"
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
        <button @click.prevent="register" class="register-button">
          CADASTRAR
        </button>
      </form>
    </div>
  </q-layout>
</template>

<script>
import ToolBar from "../components/ToolBar";
export default {
  components: { ToolBar },
  data: () => {
    return {
      type: "nutella"
    };
  },
  methods: {
    register() {
      const payload = {
        name: document.getElementById("name").value,
        email: document.getElementById("email").value,
        coin: document.getElementById("coins").value,
        type: this.type
      };

      console.log(payload);

      //send request to server
    }
  }
};
</script>

<style>
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
  margin-top: 10px;
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
  margin-top: 0px;
  background-color: #7a00e3;
}

.card input[type="radio"] {
  margin-right: 5px;
}

#div-radio {
  padding: 15px 0px;
  width: 200px;
}

.register-button {
  padding: 15px 0px;
  font-weight: bolder;
  font-size: 2em;
  background-color: #04d98b;
  color: #00a16f;
  border: 0;
}

.radio-button input:checked {
  background-color: violet;
}
</style>
