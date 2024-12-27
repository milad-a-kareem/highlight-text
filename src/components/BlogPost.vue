<script setup lang="ts">
import { computed } from 'vue'
import DOMPurify from 'dompurify'

const props = defineProps<{
  title: string
  content: string
  highlightText: string
}>()

const titleHtml = computed(() => {
  const regex = new RegExp(props.highlightText, 'gi')

  const html = props.title.replace(
    regex,
    (match) => `<span style="background-color: yellow;">${match}</span>`,
  )

  return DOMPurify.sanitize(html)
})

const contentHtml = computed(() => {
  const regex = new RegExp(props.highlightText, 'gi')

  const html = props.content.replace(
    regex,
    (match) => `<span style="background-color: yellow;">${match}</span>`,
  )

  return DOMPurify.sanitize(html)
})
</script>

<template>
  <div class="container">
    <h1 class="title" v-html="titleHtml"></h1>
    <p class="content" v-html="contentHtml"></p>
  </div>
</template>

<style scoped>
.container {
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 8px;
  margin-block-end: 20px;
}

.title {
  margin-block-end: 10px;
  font-size: 24px;
}

.content {
  font-size: 16px;
}

.highlight {
  background-color: yellow;
}
</style>
