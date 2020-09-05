<template>
  <div>
    <q-layout class="bg-mid-purple" view="lHh Lpr lFf">
      <ToolBar type="search" />

      <div class="row justify-center q-my-md">
        <div
          class="cards"
          v-infinite-scroll="getUserList"
          infinite-scroll-disabled="busy"
          infinite-scroll-distance="0"
        >
          <Card
            class="bg-dark-purple"
            :key="volunter.id"
            v-for="volunter in volunters"
            :name="volunter.name"
            :moneyQuantity="volunter.moneyQuantity"
            :id="volunter.id"
          />
        </div>
        <!-- <q-spinner color="white" size="3em" :thickness="2" /> -->
      </div>

      <router-view />
    </q-layout>
    <router-link to="/new/user">
      <button
        class="position-absolute fixed-bottom w-100 border-none py-10"
        id="new-button"
      >
        <span>Novo Voluntário</span>
      </button>
    </router-link>
  </div>
</template>

<script>
import ToolBar from "../components/ToolBar.vue";
import Card from "../components/Card.vue";
import Axios from "axios";
import infiniteScroll from "vue-infinite-scroll";
export default {
  name: "MainLayout",
  components: { Card, ToolBar },
  data() {
    return {
      pageStep: 1,
      volunters: [],
      busy: true
    };
  },
  directives: { infiniteScroll },

  methods: {
    async getUserList() {
      this.busy = true;

      const request = await Axios.get(
        `https://newschool-dashboard-coins-back.herokuapp.com/user?page=${this.pageStep}`
      );
      this.busy = false;
      this.pageStep += this.pageStep + 1;

      request.data.forEach((obj, index) => {
        let fullName = obj.name;
        fullName = fullName.split(" ");

        let shortName = [];

        if (fullName.length >= 2) {
          fullName.forEach((name, index) =>
            name.split("").length > 2 &&
            index > 0 &&
            index < fullName.length - 1
              ? shortName.push(name[0])
              : shortName.push(name)
          );
          shortName = shortName.join().replace(/,/g, " ");

          request.data[index].name = shortName;
        }
      });

      this.volunters = request.data;
    }
  },
  created() {
    this.getUserList();
  }
};
</script>
<style scoped>
.card {
  margin-top: 2px;
}

.logout__image {
  vertical-align: middle;
  width: 40px;
  height: 40px;
}
.hamburguer__menu {
  color: rgb(68, 0, 237);
}

::v-deep .q-layout {
  padding: 0px;
  margin: 0px;
  padding-bottom: 30px;
}

#new-button {
  font-size: 1.5em;
  background-color: #04d98b;
  color: #00ad77;
  font-weight: bold;
}
</style>
