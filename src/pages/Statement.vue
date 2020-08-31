<template>
  <AdminHistory />
</template>

<script>
import AdminHistory from "../components/statement/Admin/AdminHistory";

export default {
  components: { AdminHistory },
  data: () => {
    return {
      id: ""
    };
  },
  created: function() {
    this.id = this.$route.params.id;
  }
};
</script>

<style></style>
