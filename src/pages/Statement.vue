<template>
  <div>
    <Search />
    <balance :Balance="balance" />
    <input placeholder="CoinQuantity" id="coinQty" :value="0" />
    <ToggleCoins />
    <AdminHistory :changesHistory="{ changesHistory }" />
  </div>
</template>

<script>
import Balance from "../components/statement/balance/Balance";
import AdminHistory from "../components/statement/admin/AdminHistory";
import ToggleCoins from "../components/statement/balance/ToggleCoins";
import Search from "../components/statement/search/Search";
import eventBus from "../components/eventBus";

export default {
  components: { AdminHistory, Balance, ToggleCoins, Search },
  data: () => {
    return {
      id: "",
      changesHistory: [],
      balance: 0,
      countInterval: false
    };
  },
  methods: {
    async getUserInfo() {
      //Axios request to server side
      //////////////////////////////
      //pseudo request
      const info = {
        id: 1,
        balance: 20,
        adminchangesHistory: [
          {
            id: 1,
            date: "21/02/2020",
            adminName: "leo onidas",
            coins: 10
          },
          {
            id: 2,
            date: "21/02/2020",
            adminName: "leo onidas",
            coins: 20
          },
          {
            id: 3,
            date: "21/02/2020",
            adminName: "leo onidas",
            coins: -10
          }
        ]
      };

      this.balance = info.balance;
      this.changesHistory = info.adminchangesHistory;
    },

    async addCoins(qty) {
      //Send Request to server side
      this.getUserInfo();
    },
    async removeCoins(qty) {
      //Send Request to server side

      this.getUserInfo();
    },

    async startSearch(payload) {
      //Send Request to server side

      this.getUserInfo();
    }
  },
  async created() {
    this.id = this.$route.params.id;

    await this.getUserInfo();

    //add coins by event
    eventBus.$on("toggleCoins", async type => {
      const coinQuantity = document.getElementById("coinQty").value;

      type == "add"
        ? this.addCoins(coinQuantity)
        : this.removeCoins(coinQuantity);
    });

    //search history event
    eventBus.$on("startSearch", payload => {
      this.startSearch(payload);
    });
  }
};
</script>

<style></style>
