<template>
  <div class="row d-flex card items-center justify-around">

      <div class="col d-flex col-user items-center">
        <img src="~assets/person.png" alt="" height="30px" >

        <p class="text-white info col d-flex m-0">{{name}}</p>
      </div>

      <div class="col d-flex justify-end col-coin items-center">
        <img src="~assets/coin.png" alt="" height="30px">
        <p class="text-white info m-0">{{moneyQuantity}}</p>
      </div>
      <router-link :to="{ path: `/statement/${id}` }" class="router-link">
        <div class="bg-mid-purple d-flex arrow items-center ">
          <img src="~assets/arrow.png" alt="" id="arrow-image" height="35px">
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
  position: relative;
  padding-left: 10px;
  min-height: 64px;
  align-items: stretch;
  max-width: 768px;
}

.info{
  margin-left: 10px;
  font-size: 1.5em;
}

.arrow{
  display:inline-block;
  position: relative;

}

.col-user{
  padding-left: 40px;
}

.col-coin{
  padding-right: 10px;
}

.router-link{
  background-color: #8305f0;
  display: flex;
  align-items: center;
  min-height: 100%;
}
</style>
