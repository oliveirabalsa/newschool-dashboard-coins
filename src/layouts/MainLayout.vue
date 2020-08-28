<template>
  <q-layout style="background: #4e00ff" view="lHh Lpr lFf">
    <HeaderMenu />
    <Card style="margin-top: 50px" />
    <Card />
    <Card />
    <Card />
    <Card />
    <!-- <q-drawer
          @click="leftDrawerOpen = !leftDrawerOpen"
      v-model="leftDrawerOpen"
      show-if-above
      bordered
      content-class="bg-grey-1"
    >
      <q-list>
        <q-item-label
          header
          class="text-grey-8"
        >
          Essential Links
        </q-item-label>
        <EssentialLink
          v-for="link in essentialLinks"
          :key="link.title"
          v-bind="link"
        />
      </q-list>
    </q-drawer> -->

      <router-view />
  </q-layout>
</template>

<script>
import HeaderMenu from '../components/HeaderMenu.vue';
import Card from '../components/Card.vue';

export default {
  name: 'MainLayout',
  components: { Card, HeaderMenu },
  data() {},
};
</script>
<style scoped>

.logout__image {
  vertical-align: middle;
  width: 40px;
  height: 40px;
}
.hamburguer__menu {
  color: rgb(68, 0, 237);
}
.header {
  background-color: white !important;
}

</style>
