<template>
  <div>
    <Admin :key="obj.id" v-for="obj in changesHistory" :info="obj" />
  </div>
</template>

<script>
import Admin from "./Admin";

export default {
  components: { Admin },
  data: () => {
    return {
      changesHistory: []
    };
  },

  methods: {
    getUserHistory() {
      //Axios request to server side
      //////////////////////////////
      //pseudo request
      return [
        {
          id: 1,
          date: "21/02/2020",
          adminName: "leo onidas",
          coins: 100
        },
        {
          id: 2,
          date: "21/02/2020",
          adminName: "leo onidas",
          coins: -10
        },
        {
          id: 3,
          date: "21/02/2020",
          adminName: "leo onidas",
          coins: 250
        }
      ];
    }
  },

  created() {
    this.changesHistory = this.getUserHistory();
  }
};
</script>

<style></style>
