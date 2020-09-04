<template>
  <div>
    <q-layout class="bg-mid-purple" view="lHh Lpr lFf">
      <ToolBar type="search" />
      <div class="cards">
        <Card
          class="bg-dark-purple"
          :key="volunter.id"
          v-for="volunter in volunters"
          :name="volunter.name"
          :moneyQuantity="volunter.moneyQuantity"
          :id="volunter.id"
        />
      </div>
      <!-- <q-drawer
          @click="leftDrawerOpen = !leftDrawerOpen"
      v-model="leftDrawerOpen"
      show-if-above
      bordered
      content-class="bg-grey-1"
    >
      <q-list>
        <q-item-label
          header
          class="text-grey-8"
        >
          Essential Links
        </q-item-label>
        <EssentialLink
          v-for="link in essentialLinks"
          :key="link.title"
          v-bind="link"
        />
      </q-list>
    </q-drawer> -->

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
export default {
  name: "MainLayout",
  components: { Card, ToolBar },
  data() {
    return {
      volunters: []
    };
  },

  methods: {
    async getUserList() {
      const request = await Axios.get(
        "https://newschool-dashboard-coins-back.herokuapp.com/user"
      );

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
        }

        shortName = shortName.join().replace(/,/g, " ");

        request.data[index].name = shortName;
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
  padding-bottom: 30px;
}

#new-button {
  font-size: 1.5em;
  background-color: #04d98b;
  color: #00ad77;
  font-weight: bold;
}
</style>
