<template>
  <div class="d-flex column p-0">
    <div class="px-10 d-flex column mt-10">
      <p class="m-0 d-flex items-center font-bold">
        Pesquisa por data
      </p>
      <input
        type="date"
        class="bg-dark-purple text-white border-none bottom-white-line pt-10"
      />
      <input
        type="date"
        class="bg-dark-purple text-white border-none bottom-white-line pt-10"
      />
    </div>
    <div
      class=" bg-mid-purple d-flex justify-center items-center py-10"
      @click="startSearch"
    >
      <p class="m-0 p-0 font-bold font-1-5">Pesquisar</p>
      <img
        src="~assets/search.png"
        alt=""
        height="25px"
        width="25px"
        style="margin: 0px 10px"
      />
    </div>
  </div>
</template>

<script>
import eventBus from "../eventBus";
export default {
  methods: {
    startSearch() {
      eventBus.$emit("startSearch", {
        adminName: document.getElementById("adminName").value,
        startDate: document.getElementById("startDate").value,
        endDate: document.getElementById("endDate").value
      });
    }
  }
};
</script>

<style scoped>
.container {
  padding: 0px 10px;
}
</style>
