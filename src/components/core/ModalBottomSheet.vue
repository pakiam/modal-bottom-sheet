<template>
  <div class="c-modal-bottom-sheet">
    <div class="c-modal-bottom-sheet__activator">
      <slot name="activator" />
    </div>
    <template v-if="value">
      <div
        class="c-modal-bottom-sheet__overlay"
        @click="onOverlayClick"
      />
      <div class="c-modal-bottom-sheet__body">
        <slot />
      </div>
    </template>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'ModalBottomSheet',
  props: {
    value: {
      type: Boolean,
      default: false,
    },
  },
  emits: ['input'],
  methods: {
    onOverlayClick () {
      this.$emit('input')
    },
  },
})
</script>

<style lang="scss">
.c-modal-bottom-sheet {
}

.c-modal-bottom-sheet__overlay {
  position: fixed;
  z-index: 100;
  top: 0;
  right: 0;
  left: 0;
  bottom: 0;
  background-color: rgba(0, 0, 0, 0.3);
}

.c-modal-bottom-sheet__body {
  z-index: 101;
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  background-color: #fff;
  padding: 0.2rem 0;
}
</style>
