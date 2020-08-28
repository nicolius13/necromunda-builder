<template>
  <b-button
    :id="`trait-${traitType}`"
    class="traitCard mt-2"
    body-class="skillCard"
  >
    <h6 class="mb-0 text-capitalize text-info">
      {{ choosedTrait === '' ? 'Choose a Trait' : choosedTrait }}
    </h6>

    <!-- POPOVER -->
    <b-popover
      :target="`trait-${traitType}`"
      triggers="click"
      placement="top"
      boundary-padding="10"
      custom-class="traitPop"
    >
      <h5 class="text-center text-light">{{ traitType }} Traits</h5>
      <div class="separator mt-2 mb-2"></div>
      <b-card
        v-for="(trait, i) in traits"
        :key="trait.name"
        class="mt-2 mb-2"
        @click="handleChooseTrait(trait.name, i)"
      >
        <h6 class="text-center text-info text-capitalize">{{ trait.name }}</h6>
        <div class="separator mt-2 mb-2"></div>
        <p v-for="stat in trait.stat" :key="trait.name + '_' + stat.name">
          +{{ stat.change }}
          <span class="text-stat text-capitalize">{{ stat.name }}</span> and
          <span class="text-stat text-capitalize">Max {{ stat.name }}</span>
        </p>
      </b-card>
    </b-popover>
  </b-button>
</template>

<script>
import traitsInfo from '~/assets/gameInfo/traitsInfo.json';

export default {
  props: {
    traitType: {
      type: String,
      default: '',
    },
  },
  data() {
    return {
      choosedTrait: '',
      choosedTraitId: null,
      traits: traitsInfo[this.traitType],
    };
  },
  methods: {
    handleChooseTrait(traitName, traitId) {
      // change the name with the new name
      this.choosedTrait = traitName;
      // check if there is already a trait selected and save it if yes
      let oldStat;
      if (this.choosedTraitId !== null) {
        oldStat = this.traits[this.choosedTraitId].stat;
      } else {
        oldStat = null;
      }
      // change the trait ID with the new one
      this.choosedTraitId = traitId;
      // emit a event
      this.$root.$emit('changedTrait', {
        new: this.traits[traitId].stat,
        old: oldStat,
      });
      // Close all popover
      this.$root.$emit('bv::hide::popover');
    },
  },
};
</script>

<style lang="scss" scoped>
.traitCard {
  background-color: #000;
  border-color: $clr-accent2;
  transition: all 0.15s ease-in-out;

  &:hover,
  &:focus {
    background-color: $clr-dark;
    border-color: $clr-accent2;
  }

  &:focus {
    box-shadow: 0 0 0 0.2rem rgba(58, 118, 93, 0.3);
  }
}

.traitPop {
  background-color: #000;
  border-color: $clr-accent2;

  .card {
    border-color: $clr-accent2;
    cursor: pointer;
  }

  .card-body {
    color: $clr-light;
    background-color: #000;
    padding: 0.5rem 1rem;
  }
}
</style>
