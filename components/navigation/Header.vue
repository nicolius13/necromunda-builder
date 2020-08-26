<template>
  <b-navbar toggleable type="dark">
    <b-navbar-brand to="/">
      <b-img class="logo" src="~/assets/img/logo.jpg"></b-img>
    </b-navbar-brand>

    <b-navbar-toggle target="nav-sidebar"></b-navbar-toggle>

    <b-sidebar
      id="nav-sidebar"
      right
      shadow
      backdrop
      bg-variant="dark"
      text-variant="light"
    >
      <template v-slot:default="{ hide }">
        <b-container>
          <nav class="mb-3">
            <ClassesLinks
              v-for="house in houses"
              :key="house.name"
              :hide="hide"
              :house="house.name"
            />
          </nav>
        </b-container>
      </template>
    </b-sidebar>
  </b-navbar>
</template>

<script>
import houses from '../../assets/gameInfo/houses.json';

import ClassesLinks from './ClassesLinks';

export default {
  components: {
    ClassesLinks,
  },
  data() {
    return {
      houses,
    };
  },
};
</script>

<style lang="scss">
.navbar {
  background-color: #000;
  height: 80px;

  .logo {
    height: 64px;
  }
}
</style>
