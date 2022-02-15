<template>
  <div
    ref="modalBottomSheet"
    class="c-modal-bottom-sheet"
  >
    <div class="c-modal-bottom-sheet__activator">
      <slot name="activator" />
    </div>
    <Transition
      name="fade"
      :duration="250"
    >
      <div
        v-if="value"
        class="c-modal-bottom-sheet__overlay"
        @click="onOverlayClick"
      />
    </Transition>
    <Transition name="slide-fade">
      <div
        v-if="value"
        class="c-modal-bottom-sheet__body"
      >
        <slot />
      </div>
    </Transition>
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
    persistent: {
      type: Boolean,
      default: false,
    },
  },
  emits: ['input'],
  data () {
    return {
      animateTimeout: null as number | null,
      closingTimeout: null as number | null,
    }
  },
  watch: {
    value (newVal) {
      clearTimeout(this.closingTimeout as number)
      if (newVal) {
        // @TODO: move as function to composition
        // @TODO: remove duplication
        (document.querySelector('html') as HTMLElement).classList.add(
          'disable-scroll',
        )
        this.$router.push({ hash: '#modal' })
      } else {
        this.closingTimeout = setTimeout(() => {
          (document.querySelector('html') as HTMLElement).classList.remove(
            'disable-scroll',
          )
        }, 250)
        this.$router.push({ hash: '' })
      }
    },
  },
  beforeMount () {
    // @TODO: disable scroll on mobile devices
    // @TODO: remove duplication
    if (this.value) {
      // @TODO: move as function to composition
      (document.querySelector('html') as HTMLElement).classList.add(
        'disable-scroll',
      )
    } else {
      this.closingTimeout = setTimeout(() => {
        (document.querySelector('html') as HTMLElement).classList.remove(
          'disable-scroll',
        )
      }, 250)
    }
  },
  methods: {
    onOverlayClick () {
      if (this.persistent) {
        clearTimeout(this.animateTimeout as number)
        this.$nextTick(() => {
          (this.$refs.modalBottomSheet as HTMLDivElement).classList.add(
            'c-modal-bottom-sheet--animated',
          )
          this.animateTimeout = setTimeout(() => {
            (this.$refs.modalBottomSheet as HTMLDivElement).classList.remove(
              'c-modal-bottom-sheet--animated',
            )
          }, 150)
        })
        return
      }

      this.$emit('input')
    },
  },
})
</script>

<style lang="scss">
.c-modal-bottom-sheet {
  overflow: hidden;
  transition: 0.3s cubic-bezier(0.25, 0.8, 0.25, 1);
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
  position: fixed;
  bottom: 0;
  left: 0;
  right: 0;
  background-color: #fff;
  padding: 0.2rem 0;
  max-height: 90%;

  .c-modal-bottom-sheet--animated & {
    animation-duration: 0.15s;
    animation-name: animate-dialog;
    animation-timing-function: cubic-bezier(0.25, 0.8, 0.25, 1);
  }
}

// @TODO: make animations.scss
@keyframes animate-dialog {
  0% {
    transform: scale(1);
  }

  50% {
    transform: scale(1.03);
  }

  to {
    transform: scale(1);
  }
}

.slide-fade-enter-active {
  transition: all 0.3s ease-out;
}

.slide-fade-leave-active {
  transition: all 0.2s cubic-bezier(1, 0.5, 0.8, 1);
}

.slide-fade-enter-from,
.slide-fade-leave-to {
  transform: translateY(100%);
  opacity: 0;
}
</style>
