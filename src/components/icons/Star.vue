<template>
  <svg
    class="icon-star"
    width="20"
    height="20"
    :style="{
      fill: primaryColor,
      width: size,
      height: size
    }"
  >
    <defs>
      <path
        d="M3.514 11.457a1 1 0 0 1-1.45-1.05l.47-2.76-2-1.95a1 1 0 0 1 .55-1.7l2.77-.4 1.23-2.51a1 1 0 0 1 1.8 0l1.23 2.5 2.77.4a1 1 0 0 1 .55 1.71l-2 1.95.47 2.76a1 1 0 0 1-1.45 1.05l-2.47-1.3-2.47 1.3z"
        id="star"
      />
    </defs>
    <svg preserveAspectRatio="xMidYMid meet" x="0" y="0" viewBox="0 0 12 12">
      <use href="#star" />
    </svg>
  </svg>
</template>

<script>
export default {
  props: {
    primaryColor: {
      type: String,
      default: "#000"
    },
    size: {
      default: 32
    }
  }
};
</script>

<style scoped lang="scss">
.icon-star {
  transition: fill 1s ease-out;
}
</style>
