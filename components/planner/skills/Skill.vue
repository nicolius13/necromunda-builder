<template>
  <b-card class="border border-succes" body-bg-variant="dark">
    <b-row>
      <b-col>
        <h4 class="text-center">Active Skills</h4>
        <div class="separator"></div>
        <SkillCard v-for="(skill, i) in 5" :key="i" />
      </b-col>
      <b-col>
        <h4 class="text-center">Passive Skills</h4>
        <div class="separator"></div>
        <SkillCard v-for="(skill, i) in 5" :key="i" />
      </b-col>
    </b-row>
    <b-row>
      <b-col>
        <h4 class="text-center mt-3">Fighter perks</h4>
        <div class="separator"></div>
      </b-col>
    </b-row>
    <b-row>
      <b-col v-for="(perk, i) in 3" :key="i">
        <PerkCard />
      </b-col>
    </b-row>
  </b-card>
</template>

<script>
import SkillCard from './SkillCard';
import PerkCard from './PerkCard';

export default {
  components: {
    SkillCard,
    PerkCard,
  },
};
</script>

<style lang="scss" scoped></style>
