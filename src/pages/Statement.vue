<template>
  <q-layout view="lHh Lpr lFf">
    <ToolBar type="back" />
    <div class="bg-mid-purple w-100 d-flex column">
      <div class="row bg-mid-purple jutify-around headerControls d-flex column">
        <Balance :Balance="balance" class="" style="margin-top: 12px" />
        <div class="d-flex">
          <input
            class="text-white input placeholder-white "
            v-model="coinQty"
            @click="clearField"
            id="inputCoins"
          />
          <ToggleCoins class="d-flex p-0 " />
        </div>
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
          Nunca ganhou coins :/
        </p>
                <p
          v-if="!changesHistory || !changesHistory.length"
          class="font-1-5 text-white d-flex justify-center items-center m-0 w-100"
        >
          Sem histórico de transações :/
        </p>
      </div>
    </div>
  </q-layout>
</template>

<script>
import Balance from "../components/statement/Balance/Balance";
import Change from "../components/statement/change/Change";
import ToggleCoins from "../components/statement/Balance/ToggleCoins";
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
      coinQty: "0",
    };
  },
  methods: {
    async getUserInfo() {
      const money = await Axios.get(
        `https://newschool-dashboard-coins-back.herokuapp.com/user/money/${this.$route.params.id}`
      );

      const changesHistory = await Axios.get(
        `https://newschool-dashboard-coins-back.herokuapp.com/user/transactions/${this.$route.params.id}`
      );

      this.balance = money.data[0].moneyQuantity;

      this.changesHistory = changesHistory.data.reverse();
    },

    clearField(event) {
      event.target.value = "";
    },

    async toggleCoins(coinQty, type) {

      coinQty = coinQty.replace(/\D/gi, '')
     if(!coinQty){ return console.log('ta tirando')}
      const payload = {
        admin: "system",
        date: new Date().toISOString().toString(),
        user_id: this.$route.params.id.toString()
      };

      type == "add"
        ? (payload.quantity = coinQty.toString())
        : (payload.quantity = (coinQty * -1).toString());

      this.$q.loading.show()
       await Axios.post(
    'https://newschool-dashboard-coins-back.herokuapp.com/user/transactions',
    payload,
  );
      this.getUserInfo();
      this.coinQty = 0;
      this.$q.loading.hide()
    },

    async startSearch(payload) {
      //Send Request to server side
      this.getUserInfo();
    }
  },
  async created() {
    this.getUserInfo();

    //add coins by event
    eventBus.$on("toggleCoins", async (type) => {
      console.log(type)
      this.toggleCoins(this.coinQty, type)
      // type == "add"
      //   ? this.addCoins(this.coinQty, type)
      //   : this.removeCoins(this.coinQty, type);
    });

    //search history event
    eventBus.$on("startSearch", payload => {
      this.startSearch(payload);
    });
  }
};
</script>

<style scoped>
#inputCoins {
  font-size: 1.5em;
  width: 100%;
}

.headerControls {
  margin-top: 70px;
  padding: 10px;
}

.ToggleCoins {
}
</style>
