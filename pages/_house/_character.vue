<template>
  <b-container>
    <b-row class="mt-3 mb-3">
      <b-col class="d-flex align-items-end" cols="8">
        <div class="text-center">
          <b-img
            :class="isLeader ? null : 'leadVis'"
            class="leadIcon"
            src="~/assets/img/icons/classes/leader.png"
          ></b-img>
          <ClassesIcon :house="house" :character="character" :dimension="35" />
        </div>
        <h2 :class="`text-${house}`" class="text-capitalize ml-2">
          House {{ house }} : {{ character }}
          <span v-if="isLeader">Leader</span>
        </h2>
      </b-col>
      <b-col class="d-flex align-items-end justify-content-end" cols="4">
        <b-button
          class="leadBtn"
          variant="outline-primary"
          @click="isLeader = !isLeader"
          >{{ isLeader ? 'Demote Leader' : 'Promote Leader' }}</b-button
        >
      </b-col>
    </b-row>
    <b-row>
      <b-col cols="4">
        <b-row>
          <b-col>
            <!-- STATS -->
            <Stats
              :house="house"
              :character="character"
              :is-leader="isLeader"
            />
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
            <!-- TRAITS -->
            <Traits class="mt-3" />
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
import Traits from '../../components/planner/traits/Traits';
import Inventory from '../../components/planner/inventory/Inventory';

export default {
  components: {
    ClassesIcon,
    Stats,
    GeneralStats,
    SubStats,
    Skill,
    Traits,
    Inventory,
  },
  data() {
    return {
      house: this.$route.params.house,
      character: this.$route.params.character,
      isLeader: false,
    };
  },
};
</script>

<style lang="scss" scoped>
h2 {
  margin-bottom: 2px;
}

.leadBtn {
  margin-bottom: 4px;
}
.leadIcon {
  transition: opacity 0.15s ease-in-out;
}
.leadVis {
  opacity: 0;
}
</style>
