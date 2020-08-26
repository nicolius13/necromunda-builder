<template>
  <b-container>
    <b-row>
      <b-col class="d-flex mt-3 mb-3">
        <ClassesIcon :house="house" :character="character" :dimension="35" />
        <h2 :class="`text-${house}`" class="text-capitalize">
          House {{ house }} : {{ character }}
        </h2>
      </b-col>
    </b-row>
    <b-row>
      <b-col cols="4">
        <b-row>
          <b-col>
            <!-- STATS -->
            <Stats />
            <!-- GENERAL STATS -->
            <GeneralStats class="mt-3" />
            <!-- SUB-STATS -->
            <SubStats class="mt-3" />
          </b-col>
        </b-row>
      </b-col>
      <b-col cols="8">
        <b-row>
          <b-col>
            <!-- SKILLS -->
            <Skill />
            <!-- INVENTORY -->
            <Inventory class="mt-3" />
          </b-col>
        </b-row>
      </b-col>
    </b-row>
  </b-container>
</template>

<script>
import ClassesIcon from '../../components/navigation/ClassesIcon';
import Stats from '../../components/planner/Stats';
import GeneralStats from '../../components/planner/GeneralStats';
import SubStats from '../../components/planner/SubStats';
import Skill from '../../components/planner/skills/Skill';
import Inventory from '../../components/planner/inventory/Inventory';

export default {
  components: {
    ClassesIcon,
    Stats,
    GeneralStats,
    SubStats,
    Skill,
    Inventory,
  },
  data() {
    return {
      house: this.$route.params.house,
      character: this.$route.params.character,
    };
  },
};
</script>

<style lang="scss" scoped></style>
