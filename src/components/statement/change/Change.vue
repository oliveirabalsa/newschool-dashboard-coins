<template>
  <div class="column">
    <q-list>
      <q-item v-ripple class="bg-dark-purple row change-item">
        <q-item-section class="text-white col d-flex justify-center">
          <p class="col d-flex justify-center">
            {{ changeInfo.date | convertDate }}
          </p>
        </q-item-section>
        <q-item-section class="text-white">
          <p class="col d-flex justify-center m-0">
            {{ changeInfo.admin }}
          </p>
        </q-item-section>

        <q-item-section class="text-white">
          <p class="col d-flex justify-center m-0">
            {{ changeInfo.quantity }}
          </p>
        </q-item-section>
      </q-item>
    </q-list>
  </div>
</template>

<script>
import moment from "moment";
export default {
  props: ["changeInfo"],
  filters: {
    convertDate: date => {
      return moment(String(date)).format("MM/DD/YYYY");
    }
  }
};
</script>

<style scoped>
.change-item {
  margin: -4px;
}

.column {
  margin-top: 10px;
}
</style>
