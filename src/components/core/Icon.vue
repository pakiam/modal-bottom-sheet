<template>
  <div class="c-icon">
    <i
      class="c-icon__item"
      aria-hidden="true"
    >{{ name }}</i>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'Icon',
  props: {
    name: {
      type: String,
      required: true,
    },
  },
})
</script>

<style lang="scss">
.c-icon {
  display: flex;
  padding: 0.1rem;
}
.c-icon__item {
  font-family: 'Material Icons';
  font-weight: normal;
  font-style: normal;
  font-size: 0.24rem;  /* Preferred icon size */
  display: inline-block;
  line-height: 1;
  text-transform: none;
  letter-spacing: normal;
  word-wrap: normal;
  white-space: nowrap;
  direction: ltr;

  /* Support for all WebKit browsers. */
  -webkit-font-smoothing: antialiased;
  /* Support for Safari and Chrome. */
  text-rendering: optimizeLegibility;

  /* Support for Firefox. */
  -moz-osx-font-smoothing: grayscale;

  /* Support for IE. */
  font-feature-settings: 'liga';
}
</style>
