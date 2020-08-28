<template>
  <b-card class="border border-succes" bg-variant="dark">
    <h4 class="text-center">Sub-Stats</h4>
    <div class="separator mt-2 mb-2"></div>
    <div v-for="(stat, key, i) in subStats" :key="stat.name">
      <b-row
        :class="i % 2 !== 0 ? 'greenBack' : null"
        class="justify-content-around mb-2"
      >
        <b-col cols="8">
          <p>{{ stat.name }}</p>
        </b-col>
        <b-col
          v-if="key !== 'ini' && key !== 'exp'"
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
      subStats: {
        ranEv: {
          name: 'Ranged evasion',
          value: 1,
        },
        melEv: {
          name: 'Melee evasion',
          value: 1,
        },
        melPen: {
          name: 'Melee Penetration',
          value: 1,
        },
        byMelStunRes: {
          name: 'Bypass Melee Stun Resistance',
          value: 2,
        },
        healRe: {
          name: 'Healing Received',
          value: 104,
        },
        critRes: {
          name: 'Critical Hit Resistance',
          value: 1,
        },
        stressRes: {
          name: 'Stress Resistance',
          value: 3,
        },
        stunRes: {
          name: 'Stun Resistance',
          value: 3,
        },
        ranPen: {
          name: 'Ranged Penetration',
          value: 1,
        },
        exp: {
          name: 'Experience Bonus ??',
          value: 6,
        },
        ini: {
          name: 'Initiative ??',
          value: 51,
        },
        hitRes: {
          name: 'Hit Resistance',
          value: 1,
        },
        melHitPre: {
          name: 'Melee Hit Precision',
          value: 1,
        },
        byMelEv: {
          name: 'Bypass Melee Evasion',
          value: 1,
        },
        ranHitPre: {
          name: 'Ranged Hit Precision',
          value: 1,
        },
        byRanEv: {
          name: 'Bypass Ranged Evasion',
          value: 1,
        },
        melCritChan: {
          name: 'Melee Critical Hit Chance',
          value: 1,
        },
        ranCritChan: {
          name: 'Ranged Critical Hit Chance',
          value: 1,
        },
      },
    };
  },

  created() {
    // AGILITY change
    this.$root.$on('agiChange', agi => {
      // Ranged evasion = agi * 1
      this.subStats.ranEv.value = agi;
      // Melee evasion = agi * 1
      this.subStats.melEv.value = agi;
    });
    // STRENGTH change
    this.$root.$on('strChange', str => {
      // Melee Penetration = str * 1
      this.subStats.melPen.value = str;
      // Bypass melee stun resistance = str * 2
      this.subStats.byMelStunRes.value = str * 2;
    });
    // TOUGHNESS change
    this.$root.$on('touChange', tou => {
      // Healing received = 100% + toughness * 4
      this.subStats.healRe.value = 100 + tou * 4;
      // Critical hit resistance = tou * 1
      this.subStats.critRes.value = tou;
    });

    // WILLPOWER change
    this.$root.$on('wilChange', wil => {
      // Stress resistance = wil * 3
      this.subStats.stressRes.value = wil * 3;
      // Stun resistance = wil * 3
      this.subStats.stunRes.value = wil * 3;
    });
    // INTELLIGENCE change
    this.$root.$on('intChange', int => {
      // Ranged penetration = int * 1
      this.subStats.ranPen.value = int;
      // Experience bonus = 5 + int * 1 ??
      this.subStats.exp.value = 5 + int;
    });
    // ALETRNESS change
    this.$root.$on('aleChange', ale => {
      // Initiative = 50 + ale * 1 ??
      this.subStats.ini.value = 50 + ale;
      // Hit resistance = ale * 1
      this.subStats.hitRes.value = ale;
    });

    // MELEE PROWESS change
    this.$root.$on('melChange', mel => {
      // Melee hit precision = mel * 1
      this.subStats.melHitPre.value = mel;
      // Bypass melee evasion = mel * 1
      this.subStats.byMelEv.value = mel;
    });
    // RANGED APTITUDE change
    this.$root.$on('ranChange', ran => {
      // Ranged hit precision = ran * 1
      this.subStats.ranHitPre.value = ran;
      // Bypass ranged evasion = ran * 1
      this.subStats.byRanEv.value = ran;
    });
    // ACCURACY change
    this.$root.$on('accChange', acc => {
      // Melee critical hit chance = acc * 1
      this.subStats.melCritChan.value = acc;
      // ranged critical hit chance = acc * 1
      this.subStats.ranCritChan.value = acc;
    });
  },
};
</script>

<style lang="scss" scoped>
.separator-left {
  margin-left: -15px;
  width: calc(100% + 30px);
}
</style>
