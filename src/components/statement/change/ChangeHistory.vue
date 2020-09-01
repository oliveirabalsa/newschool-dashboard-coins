<template>
  <div>
    <div :key="changeH.id" v-for="changeH in changesHistory" :changeH="changeH">
      <Change
        :key="changeH.id"
        v-for="changeS in changeH"
        :changeSub="changeS"
      />
    </div>
  </div>
</template>

<script>
import Change from "./Change";

export default {
  components: { Change },
  props: ["changesHistory"]
};
</script>

<style></style>
