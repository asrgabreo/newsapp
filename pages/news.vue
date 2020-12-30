<template>
  <div>
    <v-container>
      <v-flex xs12 pb-6>
        <h2>News</h2>
      </v-flex>
      <v-flex
        xs12
        pb-3
        sm6
        offset-sm3
        v-for="(article, index) in articles"
        :key="index"
      >
        <v-card>
          <img :src="article.urlToImage" height="200px" width="100%" />

          <v-card-title primary-title>
            <div class="headline">{{ article.title }}</div>
          </v-card-title>
          <v-card-text>
            {{ article.content }}
          </v-card-text>
          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn flat :href="article.url" target="_blank">Open</v-btn>
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
      const { articles } = await app.$axios.$get(
        "http://newsapi.org/v2/top-headlines?country=in&apiKey=e5f399e7b36946f7b316fa4f84a0eede"
      );
      return { articles };
    } catch (err) {
      console.log(err);
    }
  },
};
</script>