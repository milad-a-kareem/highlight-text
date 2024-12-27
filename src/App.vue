<script setup lang="ts">
import { ref, computed } from 'vue'
import BlogPost from './components/BlogPost.vue'

const search = ref('')

const articles = ref([
  {
    title: 'If You Can Answer These 7 Questions Correctly You are Decent at JavaScript',
    content:
      'JavaScript can be a little tricky sometimes, even when you are dealing with simple-looking problems. Here are seven questions that test different parts of JavaScript. They look easy, but they can catch you off guard! If you can answer these, you have got a good handle on JavaScript!',
  },
  {
    title: 'Why Experienced Programmers Fail Coding Interviews',
    content:
      'A friend of mine recently joined a FAANG company as an engineering manager, and found themselves in the position of recruiting for engineering candidates.',
  },
  {
    title: 'How to Give Feedback to High Performers on Your Team',
    content:
      'No one is perfect and that applies to high performers on your team too. They may be doing excellent work or exceeding your expectations, but that doesn’t make them flawless or leave them with no room for improvement or areas of growth.',
  },
  {
    title: 'How to Write a Simple Money Transfer Service That Is Thread-Safe and Lock-Free',
    content:
      'Money transfer services are at the core of the modern financial system, making sure that billions of transactions occur seamlessly across the globe. But when you delve into the actual code behind such services, one of the most challenging aspects is ensuring thread safety without compromising performance. Thread-safe programming, particularly in concurrent systems, comes with complexities — especially when you try to implement it without locks.',
  },
  {
    title: 'Why I Stopped Using Else in Code',
    content:
      'One change that can make a big difference in the readability and maintainability of C# code is avoiding the else keyword. This might seem unusual for junior developers, but by removing else, the code becomes easier to read and maintain.',
  },
  {
    title: '10 Habits of Great Software Engineers',
    content:
      'Great developers tend to have a lot of little habits that they don’t teach in Computer Science courses or web development bootcamps, and these 10 habits will make you stand out.',
  },
  {
    title: '7 Leadership Mistakes That Limit Team’s Growth',
    content:
      'Business-related mistakes do not go unnoticed. Mistakes that concern the team’s growth, though, are hardly discussed or given proper attention.',
  },
  {
    title: '9 Laws That Every Software Developer Should Know',
    content:
      'In software development, there are numerous guidelines and observations referred to as laws or principles. While these are not strict formulas that hold universally in all situations, they provide important frameworks that influence the development process. These principles can significantly impact the productivity of organizations, teams, and individuals. It’s valuable for anyone involved in software to be familiar with them.',
  },
  {
    title: 'Desires of Software Development',
    content:
      'When multiple people desire the same thing, it leads to rivalry and conflict. Effort is spent to compete with rivals and not on improvement. Monopolies can focus resources on long term benefits without worrying about rivals.',
  },
  {
    title: 'What Are Micro-Frontends Really For?',
    content:
      'The concept of micro-frontends first caught my attention a few years ago. After reading about it, I was perplexed. Unfortunately, I had the bad luck of finding and consulting sources that didn’t quite grasp the concept themselves. It seemed like people were attempting to jump on the microservices bandwagon, but for the frontend. Consequently, I dismissed it as a viable idea.',
  },
])

const filteredArticles = computed(() => {
  return articles.value.filter((article) => {
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
    <input class="search-input" type="text" v-model="search" placeholder="Search..." />
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
  line-height: 1.5;
  margin-block-end: 20px;
}

main {
  flex: 1;
  gap: 20px;
  display: flex;
  flex-direction: column;
}

.search-input {
  height: 60px;
  width: 100%;
  padding: 20px;
  display: flex;
  font-size: 16px;
  border-radius: 8px;
  border: 1px solid #ccc;
}
</style>
