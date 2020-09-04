<template>
  <div>
    <!-- toolbar with one input for search user -->
    <div v-if="type == 'search'">
      <q-header class="bg-white text-dark-purple m-0">
        <q-toolbar class="m-0">
          <q-btn dense flat round icon="menu" @click="left = !left" />
          <input
            type="text"
            class="input-search w-100 text-dark-purple"
            placeholder="Pesquisar aluno"
          />
          <img
            src="~assets/search-purple.png"
            alt=""
            height="25px"
            class="p-10"
          />
        </q-toolbar>
      </q-header>

      <q-drawer show-if-above v-model="left" bordered>
        <div class="bg-mid-purple h-100 text-white">
          <div class="d-flex column bg-dark-purple" id="sidebar-items">
            <!--search card -->
            <div class="d-flex column p-0">
              <button
                class="d-flex bg-mid-purple border-none items-center"
                @click="left = false"
              >
                <p class="p-0 m-0 text-white">Bem Vindo!</p>
                <img
                  src="~assets/arrow-white-inverted.png"
                  alt=""
                  height="30px"
                  class="p-10 ml-auto"
                />
              </button>

              <div class="px-10 d-flex column mt-10">
                <p class="m-0 d-flex items-center font-bold">
                  Pesquisa por data
                </p>
                <input
                  type="date"
                  class="bg-dark-purple text-white border-none bottom-white-line pt-10"
                />
                <input
                  type="date"
                  class="bg-dark-purple text-white border-none bottom-white-line pt-10"
                />
              </div>
              <div
                class=" bg-mid-purple d-flex justify-center items-center py-10"
              >
                <p class="m-0 p-0 font-bold font-1-5">Pesquisar</p>
                <img
                  src="~assets/search.png"
                  alt=""
                  height="25px"
                  width="25px"
                  style="margin: 0px 10px"
                />
              </div>
            </div>

            <div
              class="p-10 d-flex position-absolute bg-dark-purple"
              id="div-logout"
            >
              <p class="m-0 d-flex items-center font-bold">Sair</p>
              <img
                src="~assets/logout-white.png"
                alt=""
                height="30px"
                class="ml-auto"
              />
            </div>
          </div>
        </div>
        <!-- drawer content -->
      </q-drawer>

      <q-page-container>
        <router-view />
      </q-page-container>
    </div>

    <div v-if="type == 'back'">
      <q-header class="bg-white text-dark-purple m-0">
        <q-toolbar class="m-0 p-0">
          <router-link to="/">
            <button class="border-none bg-white">
              <img src="~assets/arrow-inverted.png" alt="" height="30px" />
            </button>
          </router-link>
        </q-toolbar>
      </q-header>
    </div>
  </div>
</template>

<script>
export default {
  props: ["type"],
  data() {
    return {
      left: false
    };
  },
  created() {
    this.$q.iconSet.arrow.dropdown = "";
  }
};
</script>
<style scoped>
.logout__image {
  vertical-align: middle;
  width: 40px;
  height: 40px;
}
.hamburguer__menu {
  color: rgb(68, 0, 237);
}
.header {
  background-color: white !important;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.input-search {
  background-color: white;
  border: 0;
  border-bottom: solid 2px #7a00e3;
  margin-top: -10px;
  color: #7a00e3;
}

.input-search::placeholder {
  color: #7a00e3;
}

#div-logout {
  bottom: 0;
  left: 0;
  right: 0;
  padding: 10px;
}

.search-icon {
  margin-left: 10px;
}

.toolbar-menu {
  padding: 0;
  margin: 0;
  display: flex;
  padding: 10px 30px;
  justify-content: center;
}

#div-drop-down {
  padding: 10px;
}

.sidebar-items {
  padding: 10px 0px;
}

input[type="date"]::-webkit-calendar-picker-indicator {
  color: rgba(255, 255, 255, 0);
  opacity: 1;
  display: block;
  background: url("https://i.ibb.co/j4mr2r9/calendar.png") no-repeat;
  width: 10px;
  height: 10px;
  border-width: thin;
}

body {
  color: black;
}
</style>
