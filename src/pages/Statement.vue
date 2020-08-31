<template>
  <div>
    <balance :Balance="balance" />
    <input placeholder="CoinQuantity" id="coinQty" :value="0" />
    <ToggleCoins />
    <AdminHistory :changesHistory="{ changesHistory }" />
  </div>
</template>

<script>
import Balance from "../components/statement/Balance/Balance";
import AdminHistory from "../components/statement/Admin/AdminHistory";
import ToggleCoins from "../components/statement/Balance/ToggleCoins";
import eventBus from "../components/eventBus";

export default {
  components: { AdminHistory, Balance, ToggleCoins },
  data: () => {
    return {
      id: "",
      changesHistory: [],
      balance: 0,
      countInterval: false
    };
  },
  methods: {
    getUserInfo() {
      //Axios request to server side
      //////////////////////////////
      //pseudo request
      return {
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
    },

    addCoins(qty) {
      //Send Request to server side
      this.getUserInfo();
    },
    removeCoins(qty) {
      //Send Request to server side

      this.getUserInfo();
    }
  },
  async created() {
    this.id = this.$route.params.id;
    const userInfo = await this.getUserInfo();

    //get userInfo
    this.balance = userInfo.balance;
    this.changesHistory = userInfo.adminchangesHistory;

    //add coins by event
    eventBus.$on("toggleCoins", type => {
      const coinQuantity = document.getElementById("coinQty").value;

      type == "add"
        ? this.addCoins(coinQuantity)
        : this.removeCoins(coinQuantity);
    });
  }
};
</script>

<style></style>
