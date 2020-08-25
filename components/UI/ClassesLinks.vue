<template>
  <b-nav vertical>
    <h3 :class="house" class="text-capitalize">{{ house }}</h3>
    <b-button
      v-for="charact in classes"
      :key="charact.name"
      :class="`text-${house}`"
      class="classesBtn d-flex align-items-center"
      href="#link-1"
      variant="link"
      @click="hide"
    >
      <div
        :class="`bord-${house}`"
        class="svgContain d-flex align-items-center justify-content-center mr-2"
      >
        <span
          :style="{
            maskImage:
              'url(' + require(`~/assets/img/icons/${charact.name}.svg`) + ')',
          }"
          :class="`back-${house}`"
          class="svgIcon"
        ></span>
      </div>
      {{ charact.name }}
    </b-button>
  </b-nav>
</template>

<script>
import classes from '../../assets/classes.json';

export default {
  props: {
    hide: {
      type: Function,
      default: () => {},
    },
    house: {
      type: String,
      default: '',
    },
  },
  data() {
    return {
      classes,
    };
  },
};
</script>

<style lang="scss" scoped>
.classesBtn {
  &:focus {
    box-shadow: none;
  }

  .svgContain {
    padding: 0.25rem;
    border: solid 1px;
    border-radius: 50%;

    .svgIcon {
      display: inline-block;
      width: 24px;
      height: 24px;
      mask-size: cover;
    }
  }

  .bord-goliath {
    transition: all 0.15s ease-in-out;
    border-color: $clr-goliath;
  }
  .bord-esher {
    transition: all 0.15s ease-in-out;
    border-color: $clr-esher;
  }
  .bord-orlock {
    transition: all 0.15s ease-in-out;
    border-color: $clr-orlock;
  }
  &:hover .bord-goliath {
    border-color: darken($clr-goliath, 15%);
  }
  &:hover .bord-esher {
    border-color: darken($clr-esher, 15%);
  }
  &:hover .bord-orlock {
    border-color: darken($clr-orlock, 15%);
  }

  .back-goliath {
    background: $clr-goliath;
    transition: all 0.15s ease-in-out;
  }
  .back-esher {
    background: $clr-esher;
    transition: all 0.15s ease-in-out;
  }
  .back-orlock {
    background: $clr-orlock;
    transition: all 0.15s ease-in-out;
  }

  &:hover .back-goliath {
    background: darken($clr-goliath, 15%);
  }
  &:hover .back-esher {
    background: darken($clr-esher, 15%);
  }
  &:hover .back-orlock {
    background: darken($clr-orlock, 15%);
  }
}
</style>
