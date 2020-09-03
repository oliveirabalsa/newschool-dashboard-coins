<template>
  <div class="row d-flex card items-center justify-center">

      <div class="col d-flex col-user">
        <img src="~assets/person.png" alt="" height="30px" >

        <p class="text-white info col d-flex m-0">{{name}}</p>
      </div>

      <div class="col d-flex justify-end col-coin">
        <img src="~assets/coin.png" alt="" height="30px">
        <p class="text-white info m-0">{{moneyQuantity}}</p>
      </div>

      <router-link :to="{ path: `/statement/${id}` }">
        <div class="bg-mid-purple arrow d-flex items-center">
          <img src="~assets/arrow.png" alt="" height="40px">
        </div>
      </router-link>
    </div>
  </div>
</template>

<script>
export default {
  name: "Card",
  props: {
    name: {
      type: String,
      required: true
    },
    moneyQuantity: {
      type: String,
      required: true
    },
    id: {
      type: Number,
      required: true
    }
  }
};
</script>
<style scoped>
.card{
  padding-left: 10px;
  height: 65px;
}

.info{
  margin-left: 10px;
  font-size: 1.5em;
}

.arrow{
  height: 65px;
}

.col-user{
  padding-left: 40px;
}

.col-coin{
  padding-right: 10px;
}
</style>
