<template>
  <q-layout view="lHh Lpr lFf">
    <!-- <HeaderMenu /> -->
    <div class="bg-mid-purple vh-100 w-100 d-flex column">
      <div class="row bg-mid-purple jutify-center headerControls">
        <Balance
          :Balance="balance"
          class="grow-1 col"
          style="margin-top: 12px"
        />
        <input
          class="text-white input placeholder-white col inputCoin grow-1"
          v-model="coinQty"
          @click="clearField"
          id="inputCoins"
        />
        <ToggleCoins class="col" />
      </div>
      <div class="w-100">
        <p class="text-white" style="margin-left: 10px; margin-top: 15px">
          Histórico
        </p>
        <ChangeHistory
          v-if="changesHistory.length >= 1"
          :changesHistory="{ changesHistory }"
        />
        <p
          v-if="changesHistory.length <= 0"
          class="font-1-5 text-white d-flex justify-center items-center m-0 w-100"
        >
          Nunca Ganhou 1 NC na Vida!
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
import Axios from "axios";

export default {
  components: { ChangeHistory, Balance, ToggleCoins, Search, HeaderMenu },
  data: () => {
    return {
      changesHistory: [],
      balance: 0,
      countInterval: false,
      coinQty: "Quant"
    };
  },
  methods: {
    async getUserInfo() {
      const money = await Axios.get(
        `https://newschool-dashboard-coins-back.herokuapp.com/user/money/${this.$route.params.id}`
      );

      const changesHistory = await Axios.get(
        `https://newschool-dashboard-coins-back.herokuapp.com/user/transactions/${this.$route.params.id}?start=0&end=10`
      );

      this.balance = money.data[0].moneyQuantity;
      console.log(changesHistory.data);
      this.changesHistory = changesHistory.data;
    },

    clearField(event) {
      event.target.value = "";
    },

    async addCoins(coinQty) {
      //Send Request to server side
      const request = await Axios.put(
        `https://newschool-dashboard-coins-back.herokuapp.com/user/money/${this.$route.params.id}`,
        { adminName: "system", moneyQuantity: coinQty } //change adminName form system to real name later
      );

      document.getElementById("inputCoins").value = "";

      this.getUserInfo();
    },
    async removeCoins(coinQty) {
      //Send Request to server side

      this.getUserInfo();
    },

    async startSearch(payload) {
      //Send Request to server side

      this.getUserInfo();
    }
  },
  async created() {
    this.getUserInfo();

    //add coins by event
    eventBus.$on("toggleCoins", async type => {
      type == "add"
        ? this.addCoins(this.coinQty)
        : this.removeCoins(this.coinQty);
    });

    //search history event
    eventBus.$on("startSearch", payload => {
      this.startSearch(payload);
    });
  }
};
</script>

<style>
.inputCoin {
  height: 0;
  margin: 0px 10px;
  font-size: 1.5em;
  margin-top: 14px;
}

.headerControls {
  margin-top: 70px;
  padding: 10px;
}
</style>
