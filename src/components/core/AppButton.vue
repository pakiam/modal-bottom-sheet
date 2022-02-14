<template>
  <button
    :class="['c-button', `c-button--${size}`]"
    @click="onClick"
  >
    <div class="c-button__text">
      {{ text }}
    </div>
  </button>
</template>

<script lang="ts">
import { defineComponent, PropType } from 'vue'

export default defineComponent({
  name: 'AppButton',
  props: {
    text: {
      type: String,
      required: true,
    },
    size: {
      type: String,
      default: 'medium',
    },
    // can also annotate functions
    callback: Function as PropType<(id: number) => void>,
  },
  emits: ['click'],
  methods: {
    onClick () {
      this.$emit('click')
    },
  },
})
</script>

<style lang="scss">
.c-button {
  padding: 0 0.16rem;
  border-radius: 0.04rem;
  background-color: tomato;
  color: #fff;
}
.c-button--medium {
  font-size: 0.14rem;
  height: 0.36rem;
}
</style>
