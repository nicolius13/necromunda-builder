<template>
  <b-card class="border border-succes" bg-variant="dark">
    <h4 class="text-center">General Stats</h4>
    <div class="seperator mt-2 mb-2"></div>
    <b-row
      v-for="(stat, i) in genStat"
      :key="stat.name"
      :class="i % 2 !== 0 ? 'greenBack' : null"
      class="justify-content-around mb-2"
    >
      <b-col>
        <p>{{ stat.name }}</p>
      </b-col>
      <b-col
        v-if="stat.name !== 'Damage'"
        class="d-flex align-items-center justify-content-end"
      >
        <p>{{ stat.value }}</p>
      </b-col>
      <b-col v-else class="d-flex align-items-center justify-content-end">
        <p>{{ stat.min }} - {{ stat.max }}</p>
      </b-col>
    </b-row>
  </b-card>
</template>

<script>
export default {
  data() {
    return {
      genStat: [
        {
          name: 'AP',
          value: 60,
        },
        {
          name: 'MP',
          value: 65,
        },
        {
          name: 'Damage',
          min: 0,
          max: 0,
        },
        {
          name: 'Wounds',
          value: 200,
        },
      ],
    };
  },
};
</script>

<style lang="scss" scoped></style>
