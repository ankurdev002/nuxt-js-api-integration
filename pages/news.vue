<template>
  <div>
    <v-container class="d-flex flex-column">
      <v-flex xs12 pb-5>
        <h2 class="ml-6">News</h2>
      </v-flex>

      <v-flex class="d-flex flex-wrap justify-start">
        <!-- news -->
        <v-card
          class="d-flex flex-column justify-start mb-12 mr-6 ml-6"
          width="300"
          v-for="(article, i) in articles"
          :key="i"
        >
          <img
            :src="article.urlToImage"
            alt="no-image-to-show"
            width="100%"
            height="150px"
          />
          <v-card-title>{{ article.title }}</v-card-title>

          <v-card-text>
            <div>{{ article.content }}</div>
          </v-card-text>

          <v-card-actions>
            <v-btn
              fab
              absolute
              bottom
              right
              flat
              :href="article.url"
              target="_blank"
              color="orange"
            >
              Open
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-flex>
    </v-container>
  </div>
</template>

<script>
export default {
  async asyncData({ app }) {
    try {
      console.log(process.env.myVariable)
      const { articles } = await app.$axios.$get(
        `https://newsapi.org/v2/top-headlines?country=us&category=business&apiKey=${process.env.myVariable}`
      )
      return { articles }
    } catch (error) {
      console.error('Error fetching news:', error)
      return { articles: [] }
    }
  }
}
</script>
