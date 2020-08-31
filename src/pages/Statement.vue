<template>
  <div>
    <AdminHistory :changesHistory="{ changesHistory }" />
    <balance :Balance="balance" />
  </div>
</template>

<script>
import Balance from "../components/statement/Balance/Balance";
import AdminHistory from "../components/statement/Admin/AdminHistory";

export default {
  components: { AdminHistory, Balance },
  data: () => {
    return {
      id: "",
      changesHistory: [],
      balance: 0
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
    }
  },
  async created() {
    this.id = this.$route.params.id;
    const userInfo = await this.getUserInfo();

    this.balance = userInfo.balance;
    this.changesHistory = userInfo.adminchangesHistory;
  }
};
</script>

<style></style>
