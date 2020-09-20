<template>
  <div class="d-flex column p-0">
    <div class="d-flex column mt-10">
      <q-expansion-item
        expand-separator
        icon="search"
        label="Pesquisa Por Data"
      >
        <q-card>
          <q-card-section class="m-0">
            <input
              id="startDate"
              type="date"
              class="bg-dark-purple text-white border-none bottom-white-line pt-10"
            />
            <input
              id="endDate"
              type="date"
              class="bg-dark-purple text-white border-none bottom-white-line pt-10"
            />
            <!-- <input
              id="adminName"
              placeholder="Nome do admin"
              type="text"
              class="bg-dark-purple text-white border-none bottom-white-line pt-10"
            /> -->

            <div
              class=" bg-light-green d-flex justify-center items-center py-10"
              @click="startSearch"
            >
              <p class="m-0 p-0 font-bold font-1-5 text-dark-green">
                Pesquisar
              </p>
              <img
                src="~assets/search.png"
                alt=""
                height="25px"
                width="25px"
                style="margin: 0px 10px"
              />
            </div>
          </q-card-section>
        </q-card>
      </q-expansion-item>
    </div>
  </div>
</template>

<script>
import eventBus from "../eventBus";
export default {
  methods: {
    startSearch() {
      const startDate = document.getElementById("startDate").value
      const endDate = document.getElementById("endDate").value
      eventBus.$emit("startSearch", {startDate, endDate});
    }
  }
};
</script>

<style scoped>
*:focus {
  outline: none;
}

::placeholder {
  color: white;
}

.container {
  padding: 0px 10px;
}

.q-card__section {
  display: flex;
  flex-direction: column;
  padding: 0px;
  margin: 0px;
}
</style>
