<template>
  <b-card class="border border-succes" bg-variant="dark">
    <h4 class="text-center">Equipments</h4>
    <div class="seperator mt-2 mb-2"></div>
    <h5>Weapon</h5>
    <div class="separator-left"></div>
    <b-col v-for="(implant, i) in 1" :key="i">
      <Weapon />
    </b-col>
    <h5>Implants</h5>
    <div class="separator-left"></div>
    <b-col v-for="(implant, i) in 1" :key="i">
      <Implant />
    </b-col>
    <h5>Arms</h5>
    <div class="separator-left"></div>
    <b-col v-for="(implant, i) in 2" :key="i">
      <Armor />
    </b-col>
    <h5>Body</h5>
    <div class="separator-left"></div>
    <b-col v-for="(implant, i) in 1" :key="i">
      <Armor />
    </b-col>
    <h5>Legs</h5>
    <div class="separator-left"></div>
    <b-col v-for="(implant, i) in 2" :key="i">
      <Armor />
    </b-col>
  </b-card>
</template>

<script>
import Implant from './Implant';
import Armor from './Armor';
import Weapon from './Weapon';

export default {
  components: {
    Implant,
    Armor,
    Weapon,
  },
};
</script>

<style lang="scss" scoped></style>
