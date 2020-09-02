<template>
  <q-header elevated>
    <q-toolbar class="header">
      <q-btn
        flat
        dense
        class="hamburguer__menu"
        size="20px"
        icon="menu"
        aria-label="Menu"
      />
      <div>
        <img
          class="logout__image"
          src="../assets/logout (2).png"
          alt=""
          style="height: 30px; width: 30px"
        />
      </div>
    </q-toolbar>
  </q-header>

  <!-- @click="leftDrawerOpen = !leftDrawerOpen" -->
  <!-- <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      bordered
      content-class="bg-grey-1"
    > -->
  <!-- <q-list>
        <q-item-label
          header
          class="text-grey-8"
        >
          Essential Links
        </q-item-label>
        <<EssentialLink
          v-for="link in essentialLinks"
          :key="link.title"
      </q-list>
          v-bind="link"
    </q-drawer>
        /> -->
</template>

<script>
export default {
  name: "HeaderMenu"
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
  display: flex;
  justify-content: space-between;
  align-items: center;
}
body {
  color: black;
}
</style>
