<template>
  <q-layout view="lHh Lpr lFf">
    <HeaderMenu />
    <div class="bg-mid-purple vh-100 w-100 d-flex column">
      <!--<Search /> -->
      <div
        class="row bg-mid-purple jutify-center"
        style="margin-top: 70px; padding: 10px"
      >
        <Balance :Balance="balance" class="grow-1" style="margin-top: 12px" />
        <input
          style="height: 0; margin: 0px 10px; width: 10%; font-size: 1.5em; margin-top: 12px"
          class="text-white input placeholder-white"
          placeholder="Quantidade"
        />
        <ToggleCoins />
      </div>
      <div class="w-100">
        <p class="text-white" style="margin-left: 10px; margin-top: 15px">
          Histórico
        </p>
        <p>
          <ChangeHistory :changesHistory="{ changesHistory }" />
        </p>
      </div>
    </div>
  </q-layout>
</template>

<script>
import Balance from "../components/statement/balance/Balance";
import ChangeHistory from "../components/statement/change/ChangeHistory";
import ToggleCoins from "../components/statement/balance/ToggleCoins";
import Search from "../components/statement/search/Search";
import HeaderMenu from "../components/HeaderMenu";
import eventBus from "../components/eventBus";

export default {
  components: { ChangeHistory, Balance, ToggleCoins, Search, HeaderMenu },
  data: () => {
    return {
      id: "",
      changesHistory: [],
      balance: 0,
      countInterval: false,
      coinQty: 0
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
