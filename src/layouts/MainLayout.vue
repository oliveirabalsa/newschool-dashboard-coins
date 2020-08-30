<template>
  <q-layout style="background: #4e00ff" view="lHh Lpr lFf">
    <HeaderMenu />
    <Card name="Teste" moneyQuantity="100" style="margin-top: 50px" />
    <Card
    :key="volunter.id"
    v-for="volunter in volunters"
    :setValue="setValue"
    :name="volunter.name"
    :moneyQuantity="volunter.moneyQuantity"
     />
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
  data() {
    return {
      volunters: [
        {
          id: 1,
          name: 'Leonardo',
          moneyQuantity: '250',
        },
        {
          id: 2,
          name: 'Bianca',
          moneyQuantity: '250',
        }, {
          id: 3,
          name: 'Lucas',
          moneyQuantity: '250',
        }, {
          id: 4,
          name: 'Thiago',
          moneyQuantity: '250',
        }, {
          id: 5,
          name: 'Guilherme',
          moneyQuantity: '250',
        },

      ],
    };
  },
  methods: {
    // eslint-disable-next-line no-unused-vars
    setValue() {
      console.log('oi');
      // this.volunters[volunter].moneyQuantity = value;
      // console.log(this.volunters[volunter]);
    },
  },
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
