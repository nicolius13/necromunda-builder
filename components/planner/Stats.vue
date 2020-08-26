<template>
  <b-card class="border border-succes" body-bg-variant="dark">
    <b-row>
      <b-col>
        <h4 class="text-center">Stats</h4>
      </b-col>
      <b-col>
        <p>15 points left</p>
      </b-col>
    </b-row>
    <div class="separator mt-2 mb-2"></div>

    <b-row
      v-for="(attribut, i) in attributs"
      :key="attribut.name"
      class="justify-content-around mb-2"
    >
      <b-col>
        <p>{{ attribut.name }}</p>
      </b-col>
      <b-col class="d-flex align-items-center justify-content-end">
        <b-icon-caret-left-fill></b-icon-caret-left-fill>
        <p>{{ attribut.value }} / {{ attribut.max }}</p>
        <b-icon-caret-right-fill></b-icon-caret-right-fill>
      </b-col>
      <div v-if="i === 2 || i === 5" class="separator-left mt-2 mb-2"></div>
    </b-row>
  </b-card>
</template>

<script>
import { BIconCaretLeftFill, BIconCaretRightFill } from 'bootstrap-vue';

export default {
  components: {
    BIconCaretLeftFill,
    BIconCaretRightFill,
  },
  data() {
    return {
      attributs: [
        {
          name: 'Agility',
          value: 4,
          max: 12,
        },
        {
          name: 'Strength',
          value: 4,
          max: 12,
        },
        {
          name: 'Toughness',
          value: 4,
          max: 12,
        },
        {
          name: 'Willpower',
          value: 4,
          max: 12,
        },
        {
          name: 'Intelligence',
          value: 4,
          max: 12,
        },
        {
          name: 'Alertness',
          value: 4,
          max: 12,
        },
        {
          name: 'Melee Prowess',
          value: 4,
          max: 12,
        },
        {
          name: 'Ranged Aptitude',
          value: 4,
          max: 12,
        },
        {
          name: 'Accuracy',
          value: 4,
          max: 12,
        },
      ],
    };
  },
};
</script>

<style lang="scss" scoped>
.separator-left {
  margin: 0 15px;
}
</style>
