<script setup lang="ts">
import { ref, onMounted, onBeforeUnmount } from 'vue'
import { gsap } from 'gsap'

const title = ref<HTMLElement | null>(null)

let tween: gsap.core.Tween | null = null

onMounted(() => {
  if (!title.value) return

  tween = gsap.from(title.value, {
    opacity: 0,
    y: -100,
    duration: 1,
    ease: 'power3.out',
  })
})

onBeforeUnmount(() => {
  tween?.kill()
})
</script>

<template>
  <h1 ref="title">Welcome to the Landing Page</h1>
</template>
