<script setup lang="ts">
/**
 * Logo Salento.dev servito dall'addon, così rispetta il `base` della build.
 * `variant` è il nome del file in assets/logo senza estensione.
 */
import { computed } from 'vue'

const logos = import.meta.glob<string>('../assets/logo/*.svg', { eager: true, query: '?url', import: 'default' })

const props = withDefaults(defineProps<{ variant?: string }>(), {
  variant: 'stacked-symbol-white-on-dark',
})

const src = computed(() => logos[`../assets/logo/${props.variant}.svg`])
</script>

<template>
  <img :src="src" alt="Salento.dev">
</template>
