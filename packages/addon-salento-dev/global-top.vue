<script setup lang="ts">
/**
 * Transizione "console", dal design system del sito:
 * - le staffe d'angolo della tela si stringono e tornano larghe (come <x-ui.corners hover>, 0.25s power2.out)
 * - le etichette .eyebrow si "decifrano" come il testo della vecchia landing (decripted-text.js)
 * Con prefers-reduced-motion resta solo la dissolvenza.
 */
import { useNav } from '@slidev/client'
import { nextTick, ref, watch } from 'vue'

const { currentSlideNo, isPrintMode } = useNav()
const pulse = ref(0)
const CHARS = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789#$%&*/<>_'

function reducedMotion() {
  return typeof window !== 'undefined' && window.matchMedia('(prefers-reduced-motion: reduce)').matches
}

function decrypt(el: HTMLElement) {
  const original = el.dataset.text ?? el.textContent ?? ''
  el.dataset.text = original
  let frame = 0
  const frames = 14
  const timer = setInterval(() => {
    frame++
    const revealed = Math.floor((frame / frames) * original.length)
    el.textContent = original
      .split('')
      .map((ch, i) => (i < revealed || ch === ' ' || ch === '·' ? ch : CHARS[Math.floor(Math.random() * CHARS.length)]))
      .join('')
    if (frame >= frames) {
      clearInterval(timer)
      el.textContent = original
    }
  }, 28)
}

watch(currentSlideNo, async (no) => {
  if (isPrintMode.value || reducedMotion())
    return
  pulse.value++
  await nextTick()
  // lascia partire la transizione della slide prima di decifrare
  setTimeout(() => {
    document
      .querySelectorAll<HTMLElement>(`.slidev-page-${no} .eyebrow`)
      .forEach(decrypt)
  }, 120)
})
</script>

<template>
  <div v-if="!isPrintMode" :key="pulse" class="console-frame" :class="{ pulse: pulse > 0 }" aria-hidden="true">
    <i class="tl" /><i class="tr" /><i class="bl" /><i class="br" />
  </div>
</template>

<style scoped>
.console-frame {
  position: absolute;
  inset: 14px;
  pointer-events: none;
  z-index: 20;
}

.console-frame i {
  position: absolute;
  width: 14px;
  height: 14px;
  border-color: oklch(45% 0.017 213.2);
  border-style: solid;
}

.tl { top: 0; left: 0; border-width: 1px 0 0 1px; --x: 1; --y: 1; }
.tr { top: 0; right: 0; border-width: 1px 1px 0 0; --x: -1; --y: 1; }
.bl { bottom: 0; left: 0; border-width: 0 0 1px 1px; --x: 1; --y: -1; }
.br { bottom: 0; right: 0; border-width: 0 1px 1px 0; --x: -1; --y: -1; }

/* Aggancio: le staffe si stringono di 8px, si accendono di cyan e tornano al loro posto */
.pulse i {
  animation: lock 0.5s cubic-bezier(0.33, 1, 0.68, 1);
}

@keyframes lock {
  0% {
    transform: translate(0, 0);
  }
  40% {
    transform: translate(calc(var(--x) * 8px), calc(var(--y) * 8px));
    border-color: #20d0ed;
  }
  100% {
    transform: translate(0, 0);
  }
}

@media (prefers-reduced-motion: reduce) {
  .pulse i {
    animation: none;
  }
}
</style>
