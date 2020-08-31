<template>
  <form action="">
    <input placeholder="Nome Admin" value="" id="adminName" />
    <input
      placeholder="Data Inicial"
      class="textbox-n"
      type="text"
      onfocus="(this.type='date')"
      id="startDate"
    />
    <input
      placeholder="Data Final"
      class="textbox-n"
      type="text"
      onfocus="(this.type='date')"
      id="endDate"
    />
    <button @click.prevent="startSearch">Buscar</button>
  </form>
</template>

<script>
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
