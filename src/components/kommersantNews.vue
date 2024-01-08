<script>
import axios from 'axios'

export default {
  data() {
    return {
      headlines: []
    }
  },
  mounted() {
    this.fetchHeadlines()
  },
  methods: {
    async fetchHeadlines() {
      try {
        const response = await axios.get('https://www.kommersant.ru/')
        this.headlines = this.extractHeadlines(response.data)
      } catch (error) {
        console.error('Error fetching headlines:', error)
      }
    },
    extractHeadlines(html) {
      const parser = new DOMParser()
      const doc = parser.parseFromString(html, 'text/html')
      const headlineElements = doc.querySelectorAll('.top_news__name')

      return Array.from(headlineElements).map((element) => {
        const linkElement = element.querySelector('a')
        const title = element.textContent.trim()
        const link = linkElement
          ? 'https://www.kommersant.ru/' + linkElement.getAttribute('href')
          : ''

        return {
          title,
          link
        }
      })
    }
  }
}
</script>

<template>
    <div class="grid gap-3 p-4">
  <div
    class="relative bg-white border border-slate-100 rounded-2xl p-8 cursor-pointer hover:-translate-y-2 hover:shadow-xl transition-all"
  >
    <h2>Новости Коммерсантъ</h2>
    <ul>
      <li v-for="(headline, index) in headlines" :key="index">
        <a :href="headline.link" target="_blank">{{ headline.title }}</a>
      </li>
    </ul>
  </div>
</div>
</template>
