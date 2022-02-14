<template>
  <div class="c-tile">
    <div class="c-tile__icon">
      <Icon :name="tile.icon" />
    </div>
    <div class="c-tile__text">
      {{ tile.text }}
    </div>
  </div>
</template>

<script lang="ts">
import Icon from '@/components/core/Icon.vue'
import { defineComponent, PropType } from 'vue'

interface Tile {
  icon: string
  text: string
}

export default defineComponent({
  name: 'Tile',
  props: {
    tile: {
      type: Object as PropType<Tile>,
      required: true,
    },
    // can also annotate functions
    // callback: Function as PropType<(id: number) => void>,
  },
  components: {
    Icon,
  },
})
</script>

<style lang="scss">
.c-tile {
  display: flex;
  flex-flow: row wrap;
  align-items: center;
  width: 100%;
  padding: 0.1rem;
  cursor: pointer;
  background-color: rgba(0, 0, 0, 0);
  transition: background-color ease-in-out 0.2s;

  &:hover{
    background-color: rgba(0, 0, 0, 0.12);
  }
}

.c-tile__icon {
  margin-right: 0.32rem;
}

.c-tile__text {
  flex: 1;
  text-align: left;
}
</style>
