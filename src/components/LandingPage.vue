<script setup lang="ts">
import { ref, onMounted, onBeforeUnmount } from 'vue'
import { gsap } from 'gsap'
import '../assets/gsap.css'

const title = ref<HTMLElement | null>(null)
const green = ref<HTMLElement | null>(null)
const purple = ref<HTMLElement | null>(null)
const blue = ref<HTMLElement | null>(null)
//const boxes = ref<HTMLElement | null>(null)

let tween: gsap.core.Tween | null = null
let tl: gsap.core.Timeline | null = null

// And this is a Timeline, containing three sequenced tweens

onMounted(() => {
  if (!title.value || !green.value || !blue.value || !purple.value) return

  tween = gsap.from(title.value, {
    opacity: 0,
    y: -100,
    duration: 1,
    ease: 'power3.out',
  })

  tl = gsap
    .timeline({ repeat: -1, yoyo: true })
    .to(green.value, { duration: 1, rotation: -360 })
    .to(blue.value, { duration: 2, x: -100, ease: 'elastic.out' })
    .to(purple.value, { duration: 2, rotation: 360, x: 100, ease: 'expo.out' })
})

onBeforeUnmount(() => {
  tween?.kill()
  tl?.kill()
})
</script>

<template>
  <div>
    <div>
      <div ref="green" class="box green"></div>
      <div ref="blue" class="box blue"></div>
      <div ref="purple" class="box purple"></div>
    </div>
  </div>
</template>

<style scoped></style>
