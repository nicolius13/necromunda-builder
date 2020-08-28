<template>
  <b-card class="border border-succes" body-bg-variant="dark">
    <b-row>
      <b-col>
        <h4 class="text-center">Stats</h4>
      </b-col>
      <b-col>
        <p>{{ pointLeft }} points left</p>
      </b-col>
    </b-row>
    <div class="separator mt-2 mb-2"></div>

    <b-row
      v-for="(attribut, key, i) in attributs"
      :key="attribut.name"
      class="justify-content-around mb-2"
    >
      <b-col cols="7">
        <p class="text-capitalize">{{ attribut.name }}</p>
      </b-col>
      <b-col class="d-flex align-items-center justify-content-around" cols="5">
        <b-icon-caret-left-fill
          class="caret"
          @click="substractStat(key)"
        ></b-icon-caret-left-fill>
        <p>{{ attribut.value }} / {{ attribut.max }}</p>
        <b-icon-caret-right-fill
          class="caret"
          @click="addStat(key)"
        ></b-icon-caret-right-fill>
      </b-col>
      <div v-if="i === 2 || i === 5" class="separator-left mt-2 mb-2"></div>
    </b-row>
  </b-card>
</template>

<script>
import { BIconCaretLeftFill, BIconCaretRightFill } from 'bootstrap-vue';

import houses from '../../assets/gameInfo/houses.json';
import leader from '../../assets/gameInfo/leader.json';

export default {
  components: {
    BIconCaretLeftFill,
    BIconCaretRightFill,
  },
  props: {
    house: {
      type: String,
      default: '',
    },
    character: {
      type: String,
      default: '',
    },
    isLeader: {
      type: Boolean,
      default: false,
    },
  },

  data() {
    return {
      houseStats: null,
      pointLeft: 15,
      attributs: {
        agi: {
          name: 'agility',
          baseVal: 1,
          value: 1,
          max: 10,
        },
        str: {
          name: 'strength',
          baseVal: 1,
          value: 1,
          max: 10,
        },
        tou: {
          name: 'toughness',
          baseVal: 1,
          value: 1,
          max: 10,
        },
        wil: {
          name: 'willpower',
          baseVal: 1,
          value: 1,
          max: 10,
        },
        int: {
          name: 'intelligence',
          baseVal: 1,
          value: 1,
          max: 10,
        },
        ale: {
          name: 'alertness',
          baseVal: 1,
          value: 1,
          max: 10,
        },
        mel: {
          name: 'melee prowess',
          baseVal: 1,
          value: 1,
          max: 10,
        },
        ran: {
          name: 'ranged aptitude',
          baseVal: 1,
          value: 1,
          max: 10,
        },
        acc: {
          name: 'accuracy',
          baseVal: 1,
          value: 1,
          max: 10,
        },
      },
    };
  },

  watch: {
    isLeader() {
      if (this.isLeader) {
        // add max stat to all stats as leader
        Object.values(this.attributs).forEach(stat => {
          stat.max += leader.maxStat;
        });
        // add the bonus stats as leader
        this.addBaseStats(leader.stats, true);
      } else {
        // substract the leader max stat boost to all stats
        Object.values(this.attributs).forEach(stat => {
          stat.max -= leader.maxStat;
        });
        // substract the bonus stats as leader
        this.substractBaseStats(leader.stats, true);
      }
    },
    // Watch AGILITY
    'attributs.agi.value'(newVal) {
      this.$root.$emit('agiChange', newVal);
    },
    // Watch STRENGTH
    'attributs.str.value'(newVal) {
      this.$root.$emit('strChange', newVal);
    },
    // Watch TOUGHNESS
    'attributs.tou.value'(newVal) {
      this.$root.$emit('touChange', newVal);
    },
    // Watch WILLPOWER
    'attributs.wil.value'(newVal) {
      this.$root.$emit('wilChange', newVal);
    },
    // Watch INTELLIGENCE
    'attributs.int.value'(newVal) {
      this.$root.$emit('intChange', newVal);
    },
    // Watch ALERTNESS
    'attributs.ale.value'(newVal) {
      this.$root.$emit('aleChange', newVal);
    },
    // Watch MELEE PROWESS
    'attributs.mel.value'(newVal) {
      this.$root.$emit('melChange', newVal);
    },
    // Watch RANGED APTITUDE
    'attributs.ran.value'(newVal) {
      this.$root.$emit('ranChange', newVal);
    },
    // Watch ACCURACY
    'attributs.acc.value'(newVal) {
      this.$root.$emit('accChange', newVal);
    },
  },

  created() {
    // Find the house and save the infos into houseStat
    this.houseStats = houses.find(el => el.name === this.house);
    this.addBaseStats(this.houseStats.stats);
    // listen to the Trait change
    this.$root.$on('changedTrait', $event => {
      // substract old trait stat bonus if it exist
      if ($event.old) {
        this.substractBaseStats($event.old);
      }
      // add stat bonus
      this.addBaseStats($event.new);
    });
  },

  methods: {
    // Add stats from the array given to the base stats
    addBaseStats(statObject, leader = false) {
      Object.entries(statObject).forEach(([stat, change]) => {
        if (!leader) {
          this.attributs[stat].max += change.change;
        }
        this.attributs[stat].baseVal += change.change;
        this.attributs[stat].value += change.change;
      });
    },
    // substract stats from the array given to the base stats
    substractBaseStats(statObject, leader = false) {
      Object.entries(statObject).forEach(([stat, change]) => {
        if (!leader) {
          this.attributs[stat].max -= change.change;
        }
        this.attributs[stat].baseVal -= change.change;
        this.attributs[stat].value -= change.change;
      });
    },
    // add 1 point to a given stat if there is point left and stat not at max
    addStat(stat) {
      const changedStat = this.attributs[stat];
      if (changedStat.value < changedStat.max && this.pointLeft > 0) {
        this.pointLeft--;
        changedStat.value++;
      }
    },
    // Substract 1 point to a given stat if stat not at min
    substractStat(stat) {
      const changedStat = this.attributs[stat];
      if (changedStat.value > changedStat.baseVal) {
        this.pointLeft++;
        changedStat.value--;
      }
    },
  },
};
</script>

<style lang="scss" scoped>
.separator-left {
  margin: 0 15px;
}

.caret {
  color: $clr-accent2;
  font-size: 20px;
  cursor: pointer;
  transition: all 0.15s ease-in-out;

  &:hover {
    color: darken($clr-accent2, 15%);
  }
}
</style>
