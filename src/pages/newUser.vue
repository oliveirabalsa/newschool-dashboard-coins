<template>
  <div>
    <div>Navbar foda</div>
    <form>
      <label for="name">Nome do voluntário</label>
      <input id="name" value="" />

      <label for="email">E-mail do voluntário</label>
      <input id="email" value="" />

      <label for="coins">Moedas Iniciais</label>
      <input id="coins" placeholder="Padrão: 0" value="0" type="number" />

      <label for="type">Nutella</label>
      <input type="radio" v-model="type" value="nutella" />

      <label for="type">Raíz</label>
      <input type="radio" v-model="type" value="raiz" />

      <button @click.prevent="register">Cadastrar</button>
    </form>
  </div>
</template>

<script>
export default {
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

<style></style>
