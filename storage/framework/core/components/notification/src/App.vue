<script lang="ts" setup>
import { ref } from 'vue'
import { Notification } from '.'
import type { Position, Theme } from './types'
import Expand from './components/Expand.vue'
import Footer from './components/Footer.vue'
import Hero from './components/Hero.vue'
import Installation from './components/Installation.vue'
import Others from './components/Others.vue'
import Pos from './components/Position.vue'
import Styling from './components/Styling.vue'
import Theming from './components/Theming.vue'
import Types from './components/Types.vue'
import Usage from './components/Usage.vue'
import { useSEOHeader } from './composables/useSEOHeader'
// import { toggleDarkMode, isDark } from './composables/useDarkMode'

useSEOHeader()

const expand = ref(false)
const position = ref<Position>('top-right')
const richColors = ref(false)
const closeButton = ref(false)
const theme = ref<Theme>('light')
</script>

<template>
  <div class="bg-neutral-100/66 dark:bg-neutral-900 px-4">
    <div class="container mx-auto max-w-full sm:max-w-2xl relative">
      <header class="py-20 flex-center flex-col">
        <Hero />
      </header>

      <main
        class="grid grid-cols-1 gap-8 text-xs 2xl:text-sm text-primary pb-20"
      >
        <Installation />
        <Usage />
        <Types />
        <Pos v-model:position="position" />
        <Expand v-model:expand="expand" />
        <Theming @set-theme="(newTheme: Theme) => (theme = newTheme)" />
        <Styling />
        <Others
          @set-rich-colors="richColors = true"
          @set-close-button="closeButton = true"
        />
      </main>

      <Footer />
    </div>

    <Notification
      :position="position"
      :expand="expand"
      :rich-colors="richColors"
      :close-button="closeButton"
      :theme="theme"
    />
  </div>
</template>
