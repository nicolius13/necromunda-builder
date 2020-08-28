<template>
  <div
    :class="`bord-${house}`"
    class="svgContain d-flex align-items-center justify-content-center"
  >
    <span
      :style="{
        maskImage:
          'url(' + require(`~/assets/img/icons/classes/${character}.svg`) + ')',
        height: `${dimension}px`,
        width: `${dimension}px`,
      }"
      :class="`back-${house}`"
      class="svgIcon"
    ></span>
  </div>
</template>

<script>
export default {
  props: {
    house: {
      type: String,
      default: '',
    },
    character: {
      type: String,
      default: '',
    },
    dimension: {
      type: Number,
      default: 24,
    },
  },
};
</script>

<style lang="scss" scoped>
.svgContain {
  padding: 0.25rem;
  border-radius: 50%;

  .svgIcon {
    display: inline-block;
    mask-size: cover;
  }
}
</style>
