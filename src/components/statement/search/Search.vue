<template>
  <div class="q-pa-sm" style="max-width: 300px">
    <div class="q-gutter-sm">
      <q-input placeholder="Nome Admin" value="" id="adminName" />
    </div>
    <div class="d-flex q-gutter-md">
      <input
        placeholder="Data Inicial"
        class="textbox-n date-white input"
        type="text"
        onfocus="(this.type='date')"
        id="startDate"
      />
      <input
        placeholder="Data Final"
        class="textbox-n date-white input"
        type="text"
        onfocus="(this.type='date')"
        id="endDate"
      />
      <q-btn flat class="text-white" @click.prevent="startSearch">Buscar</q-btn>
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

<style></style>
