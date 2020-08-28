<template>
  <b-card class="border border-succes" bg-variant="dark">
    <h4 class="text-center">Traits</h4>
    <div class="separator mt-2 mb-2"></div>
    <b-row class="justify-content-center align-items-center">
      <b-col class="text-center">
        <TraitCard :trait-type="'physical'" />
      </b-col>
      <b-col class="text-center">
        <TraitCard :trait-type="'mental'" />
      </b-col>
      <b-col class="text-center">
        <TraitCard :trait-type="'martial'" />
      </b-col>
    </b-row>
  </b-card>
</template>

<script>
import TraitCard from './TraitCard';

export default {
  components: {
    TraitCard,
  },
  data() {
    return {};
  },
};
</script>

<style lang="scss" scoped></style>
