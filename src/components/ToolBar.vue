<template>
  <div>
    <!-- toolbar with one input for search user -->
    <div v-if="type == 'search'">
      <q-header class="bg-white text-dark-purple m-0">
        <q-toolbar class="m-0 toolbar-menu">
          <!-- <q-btn dense flat round icon="menu" @click="left = !left" /> -->
          <input
            type="text"
            class="input-search w-100 text-dark-purple"
            placeholder="Pesquisar aluno"
            id="user"
          />
          <img
            src="~assets/search-purple.png"
            alt=""
            height="25px"
            class="p-10"
            @click="searchUser"
          />
        </q-toolbar>
      </q-header>

      <q-drawer show-if-above v-model="left" bordered>
        <div class="bg-mid-purple h-100 text-white">
          <div class="d-flex column bg-dark-purple" id="sidebar-items">
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
            <Search />
            <div
              class=" d-flex position-absolute bg-dark-purple"
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
import Search from '../components/search/Search';
import eventBus from './eventBus';

export default {
  components: { Search },
  props: ['type'],
  data() {
    return {
      left: false,
    };
  },
  created() {
    this.$q.iconSet.arrow.dropdown = '';
  },
  methods: {
    searchUser() {
      const user = document.querySelector('#user').value;
      eventBus.$emit('searchUser', user);
    },
  },
};
</script>
<style scoped>
*:focus {
    outline: none;
}
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
::v-deep .q-btn .q-icon, .q-btn .q-spinner {
  font-size: 2.7em;
  margin-right: 10px;
}

.input-search {
  background-color: white;
  border: 0;
  font-size: 18px;
  border-bottom: solid 2px #7a00e3;
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
  padding: 10px;
  justify-content: baseline;
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
