<script setup lang="ts">
import { ref, computed } from 'vue'

import BlogPost from '@/components/BlogPost.vue'
import { articles } from '@/constants/articles'

const search = ref('')

const filteredArticles = computed(() => {
  return articles.filter((article) => {
    return (
      article.title.toLowerCase().includes(search.value.toLowerCase()) ||
      article.content.toLowerCase().includes(search.value.toLowerCase())
    )
  })
})
</script>

<template>
  <header>
    <h1>Search</h1>
  </header>
  <main>
    <input class="search-bar" type="text" v-model="search" placeholder="Search..." />
    <p v-if="search.length > 0">
      <span style="font-weight: bold">
        {{ filteredArticles.length }}
        posts
      </span>
      were found
    </p>

    <div>
      <div v-for="article in filteredArticles" :key="article.title">
        <BlogPost :title="article.title" :content="article.content" :highlightText="search" />
      </div>
    </div>
  </main>
</template>

<style scoped>
header {
  margin-block-end: 20px;
}

main {
  flex: 1;
  gap: 20px;
  display: flex;
  flex-direction: column;
}

.search-bar {
  height: 60px;
  width: 100%;
  padding: 20px;
  display: flex;
  font-size: 16px;
  border-radius: 8px;
  border: 1px solid #ccc;
}
</style>
