<template>
  <section>
    <h1>Qiita 新着記事一覧</h1>
    <div
      v-for="(article, index) in articleList"
      :key="index"
    >
    <ul class="list-group">
      <li class="list-group-item">
        <a :href="article.url">{{ article.title }}</a>
      </li>
    </ul>
    </div>
  </section>
</template>

<script>
// axios
import axios from 'axios';
// qiita api URL
const BASE_URL = 'https://qiita.com/api/v2/';

export default {
  async asyncData(context) {
    try {
      const response = await axios.get(BASE_URL + 'items', {
        params: {
          page: 1,
          per_page: 10,
        }
      });
      return {
        articleList: response.data,
      };
    } catch (error) {
      console.log(error);
    }
  }
}
</script>
