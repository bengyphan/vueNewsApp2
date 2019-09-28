<template>
  <div id="app" class="container-fluid p-5 pt-1">
    <div class="row">
      <app-search v-on:newsChanged="getNews"></app-search>
    </div>
    <div>
      <label for="title">Title</label>
      <input type="radio" id="title" value="title"
        v-model="sortCriteria">
      <br>
      <label for="author">Author</label>
      <input type="radio" id="author" value="author"
        v-model="sortCriteria">
    </div>
    <div class="row">
      <app-article
        v-for="newsArticle in sortedArticles"
        v-bind:data="newsArticle">
      </app-article>
    </div>
  </div>
</template>

<script>
import Article from './components/Article.vue'
import Search from './components/Search.vue'

export default {
  data: function() {
    return {
      articles: [],
      searchQ: 'politics',
      sortCriteria: ''
    }
  },
  methods: {
    getNews: function(query) {
      var that = this;
      var url = 'https://newsapi.org/v2/everything?' +
          'q=' + 
          query + 
          '&' +
          'apiKey=333b406605bc432485a9569e2241abf4';
      var req = new Request(url);
      fetch(req)
        .then(function(response) {
          return response.json();
        })
        .then(function(data) {
          that.articles = data.articles;
        })
        
        this.searchQ = '';
        this.sortCriteria = "";
    },
    sortBy: function(arr, sortCrit) {
      return arr.sort(function(a,b) {
        if (a[sortCrit] > b[sortCrit]) return 1;
        if (a[sortCrit] < b[sortCrit]) return -1;
        return 0;
      })
    }
  },
  computed: {
    sortedArticles: function() {
      if(this.sortCriteria) {
        return this.sortBy(this.articles, this.sortCriteria);
      }
      return this.articles;
    }
  },
  components: {
    'app-article': Article,
    'app-search': Search
  },
  mounted: function(){
    this.getNews(this.searchQ);
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
