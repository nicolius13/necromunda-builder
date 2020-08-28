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
      v-for="(attribut, i) in attributs"
      :key="attribut.name"
      class="justify-content-around mb-2"
    >
      <b-col cols="7">
        <p class="text-capitalize">{{ attribut.name }}</p>
      </b-col>
      <b-col class="d-flex align-items-center justify-content-around" cols="5">
        <b-icon-caret-left-fill
          class="caret"
          @click="substractStat(attribut.name)"
        ></b-icon-caret-left-fill>
        <p>{{ attribut.value }} / {{ attribut.max }}</p>
        <b-icon-caret-right-fill
          class="caret"
          @click="addStat(attribut.name)"
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
      attributs: [
        {
          name: 'agility',
          baseVal: 1,
          value: 1,
          max: 10,
        },
        {
          name: 'strength',
          baseVal: 1,
          value: 1,
          max: 10,
        },
        {
          name: 'toughness',
          baseVal: 1,
          value: 1,
          max: 10,
        },
        {
          name: 'willpower',
          baseVal: 1,
          value: 1,
          max: 10,
        },
        {
          name: 'intelligence',
          baseVal: 1,
          value: 1,
          max: 10,
        },
        {
          name: 'alertness',
          baseVal: 1,
          value: 1,
          max: 10,
        },
        {
          name: 'melee prowess',
          baseVal: 1,
          value: 1,
          max: 10,
        },
        {
          name: 'ranged aptitude',
          baseVal: 1,
          value: 1,
          max: 10,
        },
        {
          name: 'accuracy',
          baseVal: 1,
          value: 1,
          max: 10,
        },
      ],
    };
  },

  watch: {
    isLeader() {
      if (this.isLeader) {
        // add max stat to all stats as leader
        this.attributs.forEach(stat => {
          stat.max += leader.maxStat;
        });
        // add the bonus stats as leader
        this.addBaseStats(leader.stats, true);
      } else {
        // substract the leader max stat boost to all stats
        this.attributs.forEach(stat => {
          stat.max -= leader.maxStat;
        });
        this.substractBaseStats(leader.stats, true);
      }
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
    addBaseStats(statArray, leader = false) {
      this.attributs.forEach(stat => {
        statArray.forEach(changingStat => {
          if (stat.name === changingStat.name) {
            if (!leader) {
              stat.max += changingStat.change;
            }
            stat.baseVal += changingStat.change;
            stat.value += changingStat.change;
          }
        });
      });
    },
    // substract stats from the array given to the base stats
    substractBaseStats(statArray, leader = false) {
      this.attributs.forEach(stat => {
        statArray.forEach(changingStat => {
          if (stat.name === changingStat.name) {
            if (!leader) {
              stat.max -= changingStat.change;
            }
            stat.baseVal -= changingStat.change;
            stat.value -= changingStat.change;
          }
        });
      });
    },
    // add 1 point to a given stat if there is point left and stat not at max
    addStat(stat) {
      this.attributs.find(el => {
        if (el.name === stat) {
          if (el.value < el.max && this.pointLeft > 0) {
            this.pointLeft--;
            el.value++;
          }
        }
      });
    },
    // Substract 1 point to a given stat if stat not at min
    substractStat(stat) {
      this.attributs.find(el => {
        if (el.name === stat) {
          if (el.value > el.baseVal) {
            this.pointLeft++;
            el.value--;
          }
        }
      });
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
