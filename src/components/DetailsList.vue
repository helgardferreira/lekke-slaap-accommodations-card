<template>
  <div class="details">
    <transition-group>
      <p
        v-for="(detail, index) in details"
        :key="`${detail}`"
        :class="{
          'detail-top': index === 0,
          'detail-middle': index > 0 && index < details.length - 1,
          'detail-bottom': index === details.length - 1
        }"
      >
        <a
          v-if="detail.href"
          :href="detail.href"
          target="_blank"
          rel="noopener noreferrer"
        >
          {{ detail.text }}
        </a>
        <template v-else>
          {{ detail }}
        </template>
      </p>
    </transition-group>
  </div>
</template>

<script>
export default {
  name: "DetailsList",
  props: {
    details: {
      type: Array
    }
  }
};
</script>

<style lang="scss" scoped>
$primary-color: #f9703e;
$primary-color-dark: #f35627;
$neutral-color-white: #f5f7fa;
$neutral-color-light-grey: #e4e7eb;

.details {
  color: $neutral-color-white;
  font-weight: bold;
  font-size: 14px;
  margin: 12px;
  p {
    background: $primary-color;
    list-style-type: none;
    margin: 2px 0;
    padding: 8px;
  }
  a {
    color: $neutral-color-white;
  }
  a:visited {
    color: $neutral-color-light-grey;
  }
  a:hover {
    color: $neutral-color-white;
  }
}

.detail-top {
  border-radius: 4px 4px 0 0;
}

.detail-middle {
  border-radius: 0;
}

.detail-bottom {
  border-radius: 0 0 4px 4px;
}

.v-enter-active,
.v-leave-active {
  transition: all 0.5s ease-out;
}

.v-enter,
.v-leave-to {
  transform: translateX(-400px);
  opacity: 0;
}
</style>
