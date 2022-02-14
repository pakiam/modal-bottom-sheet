<template>
  <div class="c-list-item">
    <slot default />
  </div>
</template>

<script>
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'Listitem',
  props: {},
})
</script>

<style lang="scss">
.c-list-item {
  display: flex;
  flex-flow: row wrap;
  flex: 0 0 100%;
  width: 100%;
}
</style>
