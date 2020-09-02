<template>
  <div class="q-gutter-sm grow-1 d-flex justify-end">
    <span @click="toggleCoins('add')" class="text-white"
      ><img src="~assets/plus-2.png" style="height: 35px" />
    </span>
    <span @click="toggleCoins('sub')" class="text-white"
      ><img src="~assets/negative.png" style="height: 35px"
    /></span>
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
