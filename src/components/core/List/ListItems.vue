<template>
  <div class="c-list-items">
    <slot />
  </div>
</template>

<script>
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'Listitems',
  props: {},
})
</script>

<style lang="scss">
.c-list-items {
  display: flex;
  flex-flow: row wrap;
}
</style>
