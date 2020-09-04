<template>
  <q-layout view="lHh Lpr lFf">
    <ToolBar type="back" />
    <div class="bg-mid-purple w-100 d-flex column">
      <div class="row bg-mid-purple jutify-center headerControls">
        <Balance
          :Balance="balance"
          class="grow-1 col"
          style="margin-top: 12px"
        />
        <input
          class="text-white input placeholder-white col grow-1"
          v-model="coinQty"
          @click="clearField"
          id="inputCoins"
        />
        <ToggleCoins class="col d-flex items-end p-0" />
      </div>
      <div class="w-100">
        <p class="text-white" style="margin-left: 10px; margin-top: 15px">
          Histórico
        </p>
        <Change v-for="obj in changesHistory" :key="obj.id" :changeInfo="obj" />
        <p
          v-if="balance == 0"
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
import Change from "../components/statement/change/Change";
import ToggleCoins from "../components/statement/balance/ToggleCoins";
import Search from "../components/search/Search";
import ToolBar from "../components/ToolBar";
import eventBus from "../components/eventBus";
import Axios from "axios";

export default {
  components: { Change, Balance, ToggleCoins, Search, ToolBar },
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
      console.log(changesHistory);
      this.changesHistory = changesHistory.data;
    },

    clearField(event) {
      event.target.value = "";
    },

    async addCoins(coinQty) {
      const payload = {
        admin: "system",
        quantity: coinQty.toString(),
        date: new Date().toISOString().toString(),
        user_id: this.$route.params.id.toString()
      };

      //Send Request to server side
      await Axios.post(
        `https://newschool-dashboard-coins-back.herokuapp.com/user/transactions`,
        payload
      );

      await Axios.put(
        `https://newschool-dashboard-coins-back.herokuapp.com/user/money/${this.$route.params.id}`,
        {
          moneyQuantity: (this.coinQty + this.balance).toString()
        }
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

<style scoped>
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
