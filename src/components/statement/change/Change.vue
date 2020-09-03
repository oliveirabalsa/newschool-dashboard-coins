<template>
  <div class="column">
    <q-list>
      <q-item v-ripple class="bg-dark-purple row change-item">
        <q-item-section class="text-white col d-flex justify-center">
          <p class="col d-flex justify-center">
            {{ changeSub.date }}
          </p>
        </q-item-section>
        <q-item-section class="text-white">
          <p class="col d-flex justify-center m-0">
            {{ changeSub.adminName }}
          </p>
        </q-item-section>

        <q-item-section class="text-white">
          <p class="col d-flex justify-center m-0">
            {{ changeSub.money }}
          </p>
        </q-item-section>
      </q-item>
    </q-list>
  </div>
</template>

<script>
export default {
  props: ["changeSub"]
};
</script>

<style scoped>
.change-item {
  margin: -4px;
  padding-top: 20px;
}
</style>
