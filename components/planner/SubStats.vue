<template>
  <b-card class="border border-succes" bg-variant="dark">
    <h4 class="text-center">General Stats</h4>
    <div class="separator mt-2 mb-2"></div>
    <div v-for="(stat, i) in subStats" :key="stat.name">
      <b-row
        :class="i % 2 !== 0 ? 'greenBack' : null"
        class="justify-content-around mb-2"
      >
        <b-col cols="8">
          <p>{{ stat.name }}</p>
        </b-col>
        <b-col
          v-if="stat.name !== 'Initiative' && stat.name !== 'Experience bonus'"
          class="d-flex align-items-center justify-content-end"
          cols="4"
        >
          <p>+{{ stat.value }}%</p>
        </b-col>
        <b-col
          v-else
          class="d-flex align-items-center justify-content-end"
          cols="4"
        >
          <p>{{ stat.value }}</p>
        </b-col>
      </b-row>
      <div v-if="i === 5 || i === 11" class="separator-left mb-2"></div>
    </div>
  </b-card>
</template>

<script>
export default {
  data() {
    return {
      subStats: [
        {
          name: 'Ranged evasion',
          value: 10,
        },
        {
          name: 'Melee evasion',
          value: 10,
        },
        {
          name: 'Melee Penetration',
          value: 11,
        },
        {
          name: 'Bypass melee stun resistance',
          value: 22,
        },
        {
          name: 'Healing received',
          value: 116,
        },
        {
          name: 'Critical hit resistance',
          value: 4,
        },
        {
          name: 'Stress resistance',
          value: 30,
        },
        {
          name: 'Stun resistance',
          value: 30,
        },
        {
          name: 'Ranged penetration',
          value: 11,
        },
        {
          name: 'Experience bonus',
          value: 16,
        },
        {
          name: 'Initiative',
          value: 89,
        },
        {
          name: 'Hit resistance',
          value: 7,
        },
        {
          name: 'Melee hit precision',
          value: 12,
        },
        {
          name: 'Bypass melee evasion',
          value: 12,
        },
        {
          name: 'Ranged hit precision',
          value: 12,
        },
        {
          name: 'Bypass ranged evasion',
          value: 12,
        },
        {
          name: 'Melee critical hit chance',
          value: 4,
        },
        {
          name: 'ranged critical hit chance',
          value: 4,
        },
      ],
    };
  },
};
</script>

<style lang="scss" scoped>
.separator-left {
  margin-left: -15px;
  width: calc(100% + 30px);
}
</style>
