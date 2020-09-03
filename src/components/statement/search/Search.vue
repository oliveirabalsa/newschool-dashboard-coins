<template>
  <div class="container">
    <div class="q-gutter-sm row">
      <input
        class="input placeholder-purple"
        placeholder="Nome Admin"
        value=""
        id="adminName"
      />
    </div>
    <div class="d-flex q-gutter-md row">
      <input
        placeholder="Data Inicial"
        class="textbox-n date-white input placeholder-purple col"
        type="text"
        onfocus="(this.type='date')"
        id="startDate"
      />
      <input
        placeholder="Data Final"
        class="textbox-n date-white input placeholder-purple col"
        type="text"
        onfocus="(this.type='date')"
        id="endDate"
      />
      <div
        flat
        class="text-white d-flex items-end "
        @click.prevent="startSearch"
      >
        <img src="~assets/search.png" alt="" height="30px" />
      </div>
    </div>
  </div>
</template>

<script>
import { fasSearch } from "@quasar/extras/fontawesome-v5";
import eventBus from "../../eventBus";
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
