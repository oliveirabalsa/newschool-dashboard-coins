<template>
<div class="row">
  <div class="col bg">
    <div>
      <img class="person" src="../assets/person.png" alt="">
    </div>
    <div class="volutary__name">Voluntario</div>
    <div class="money">
      <img class="money__icon" src="../assets/coin.png" alt="newcoins">
      <p class="money__quantity">100</p>
    </div>
    <div class="drag">
      <img class="drag__image" src="../assets/down-arrow (1).png" alt="">
    </div>
  </div>
</div>
</template>

<script>
export default {
  name: 'Card',
};
</script>
<style scoped>
.bg {
    background-color: rgb(68, 0, 237);
    height: 85px;
    margin-top: 3px;
    display: flex;
    align-items: center;
    position: relative;
}
.person {
    width: 33px;
    top: 36%;
    position: absolute;
    left: 15%;
}
.volutary__name {
    right: 50%;
    color: white;
    top: 42%;
    position: absolute;
    font-size: 20px;
}
.money {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 10px;
  top: 42%;
  position: absolute;
  right: 32%;
}

.money__icon {
  width: 25px;
  height: 25px;
}

.money__quantity {
  margin: 0 0 0 5px;
  color: white;
  font-size: 20px;
}

.drag{
background: #4e00ff;
    width: 54px;
    position: absolute;
    right: 0px;
    top: 0px;
    height: 85px;
}
.drag__image {
    position: absolute;
    right: 0;
    width: 53px;
    top: 18px;
    height: 53px;
}

body{
  background: #4e00ff;
}

</style>
