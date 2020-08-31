<template>
  <div>
    <Admin :key="obj.id" v-for="obj in changesHistory" :info="obj" />
  </div>
</template>

<script>
import Admin from "./Admin";

export default {
  components: { Admin },
  props: ["changesHistory"]
};
</script>

<style></style>
