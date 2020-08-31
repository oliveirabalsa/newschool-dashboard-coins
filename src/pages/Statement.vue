<template>
  <div>{{ id }}</div>
</template>

<script>
import AdminHistory from "../components/statement/Admin/AdminHistory";

export default {
  components: [AdminHistory],
  data: () => {
    return {
      id: this.$route.query.id
    };
  }
};
</script>

<style></style>
