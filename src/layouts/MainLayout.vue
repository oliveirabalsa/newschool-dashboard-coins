<template>
  <div>
    <q-layout class="bg-mid-purple" view="lHh Lpr lFf">
      <ToolBar type="search" />

      <div class="row justify-center q-my-md">
        <div
          class="cards"
          v-infinite-scroll="getUserList"
          infinite-scroll-disabled="busy"
          infinite-scroll-distance="limit"
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
import eventBus from "../components/eventBus";
import Axios from "axios";
import infiniteScroll from "vue-infinite-scroll";
export default {
  name: "MainLayout",
  components: { Card, ToolBar },
  data() {
    return {
      page: 1,
      volunters: [],
      limit: 10,
      busy: false,
      user: "",
    };
  },
  directives: { infiniteScroll },

  methods: {
    async getUserList() {
      this.busy = true;
      this.$q.loading.show()
      let stop = 0;
      if(stop === 1) {
      return this.$q.loading.hide()
      }
      // if(stop = 0){
      setTimeout(async () => {
      const request = await Axios.get(
        `https://newschool-dashboard-coins-back.herokuapp.com/user?page=${this.page}`
      )
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
      if(!request.data.length) {
        this.$q.loading.hide()
        stop++
        return
      }
      this.$q.loading.hide()
      this.page++
      this.volunters = this.volunters.concat(request.data)
      console.log(this.volunters)
      this.busy = false;
      }, 400);
    // }
    },
  async searchUser(user) {
      const request = await Axios.get(
        `https://newschool-dashboard-coins-back.herokuapp.com/user`
      )
      if(user) {
        const userFiltered = await request.data.filter(userData => userData.name.includes(user))
        if(userFiltered.length){
        this.volunters = [];
        this.volunters = userFiltered;
        console.log(this.volunters)
        } else {
          this.getUserList()
        }
      } else {
        this.getUserList()
      }
  }


  },
  created() {
    this.getUserList();

    eventBus.$on("searchUser", (user) => {
      this.searchUser(user);
    });
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
