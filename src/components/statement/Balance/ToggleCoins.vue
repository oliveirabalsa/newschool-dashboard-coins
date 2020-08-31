<template>
  <div>
    <button @click="toggleCoins('add')">+</button>
    <button @click="toggleCoins('sub')">-</button>
  </div>
</template>

<script>
import eventBus from "../../eventBus";
export default {
  methods: {
    toggleCoins(type) {
      eventBus.$emit("toggleCoins", type);
    }
  }
};
</script>

<style></style>
