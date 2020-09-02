<template>
  <q-layout class="bg-mid-purple" view="lHh Lpr lFf">
    <HeaderMenu />
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
</template>

<script>
import HeaderMenu from "../components/HeaderMenu.vue";
import Card from "../components/Card.vue";
import Axios from "axios";
export default {
  name: "MainLayout",
  components: { Card, HeaderMenu },
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

      this.volunters = request.data;
    }
  },
  created() {
    this.getUserList();
  }
};
</script>
<style scoped>
.cards {
  margin-top: 50px;
}
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
</style>
