<template>
  <div class="home">
    <img
      alt="Vue logo"
      src="../assets/logo.png"
    >
    <!-- You can add prop `persistent` to make it unclosable from outside -->
    <ModalBottomSheet
      :value="sheet"
      @input="sheet = false"
    >
      <template #activator>
        <AppButton
          text="Открыть"
          @click="onOpen"
        />
      </template>

      <!-- <AppButton
        text="Закрыть"
        @click="sheet = false"
      /> -->

      <ListItems>
        <ListItem
          v-for="(tile, index) in tiles"
          :key="index"
        >
          <Tile :tile="tile" />
        </ListItem>
      </ListItems>
    </ModalBottomSheet>
  </div>
</template>

<script lang="ts">
import { Options, Vue } from 'vue-class-component'
import AppButton from '@/components/core/AppButton.vue'
import ModalBottomSheet from '@/components/core/ModalBottomSheet.vue'
import ListItems from '@/components/core/List/ListItems.vue'
import ListItem from '@/components/core/List/ListItem.vue'
import Tile from '@/components/core/Tile.vue'

@Options({
  data () {
    return {
      sheet: false,
      tiles: [
        { icon: 'share', text: 'Share' },
        { icon: 'link', text: 'Link' },
        { icon: 'edit', text: 'Edit' },
        { icon: 'messenger', text: 'Messenger' },
      ],
    }
  },
  components: {
    AppButton,
    ModalBottomSheet,
    ListItems,
    ListItem,
    Tile,
  },
  watch: {
    '$route.hash': {
      handler: function (newVal: string, oldVal: string) {
        if (newVal === '#modal') {
          this.sheet = true
        } else if (oldVal === '#modal') {
          this.sheet = false
        }
      },
      immediate: true,
    },
  },
  methods: {
    onOpen () {
      this.sheet = !this.sheet
    },
  },
})
export default class Home extends Vue {}
</script>

<style lang="scss">
.home {
  min-height: 1200px;
}
</style>
