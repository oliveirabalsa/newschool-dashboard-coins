<template>
  <div class="column">
    <q-list>
      <q-item v-ripple class="bg-dark-purple" style="margin: -4px">
        <q-item-section class="text-white">{{ changeSub.date }}</q-item-section>
        <q-item-section class="text-white">{{
          changeSub.adminName
        }}</q-item-section>

        <q-item-section class="text-white">{{
          changeSub.coins
        }}</q-item-section>
      </q-item>
    </q-list>
  </div>
</template>

<script>
export default {
  props: ["changeSub"]
};
</script>

<style></style>
