<template>
  <b-nav vertical>
    <h3 v-if="!landing" :class="house" class="text-capitalize">{{ house }}</h3>
    <b-button
      v-for="charact in classes"
      :key="charact.name"
      :to="`/${house}/${charact.name}`"
      :class="`text-${house}`"
      class="classesBtn d-flex align-items-center"
      variant="link"
      @click="hide"
    >
      <ClassesIcon
        :house="house"
        :character="charact.name"
        :dimension="dimension"
        class="mr-2"
      />
      {{ charact.name }}
    </b-button>
  </b-nav>
</template>

<script>
import classes from '../../assets/gameInfo/classes.json';

import ClassesIcon from './ClassesIcon';

export default {
  components: {
    ClassesIcon,
  },
  props: {
    hide: {
      type: Function,
      default: () => {},
    },
    house: {
      type: String,
      default: '',
    },
    landing: {
      type: Boolean,
      default: false,
    },
  },
  data() {
    return {
      classes,
      dimension: 24,
    };
  },
};
</script>

<style lang="scss" scoped></style>
