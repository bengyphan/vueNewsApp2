<template>
	<div id="app" class="container-fluid p-5 pt-1">
		<h1>The Daily Tabloid</h1>
		<div id="search-bar" class="row p-3 justify-items-center">
			<app-search
				v-on:newsChanged="getNews"
				class="col-12 p-0 mb-2"
			></app-search>
			<div class="d-inline-block mt-5">
				<b-form-group
					class="text-left font-weight-bold"
					label="Sort By"
					stacked
				>
					<b-form-radio v-model="sortCriteria" name="some-radios" value="title"
						>Title</b-form-radio
					>
					<b-form-radio v-model="sortCriteria" name="some-radios" value="author"
						>Author</b-form-radio
					>
				</b-form-group>
			</div>
		</div>
		<hr />
		<h3 v-if="!searchQ" class="m-5">Home</h3>
		<h3 v-else>Results for "{{ searchQ }}"</h3>
		<div class="row">
			<app-article
				v-for="newsArticle in sortedArticles"
				v-bind:key="newsArticle.id"
				v-bind:data="newsArticle"
			>
			</app-article>
		</div>
	</div>
</template>

<script>
import Article from './components/Article.vue';
import Search from './components/Search.vue';

export default {
	data: function() {
		return {
			articles: [],
			searchQ: 'politics',
			sortCriteria: '',
		};
	},
	methods: {
		getNews: function(query) {
			var that = this;
			var url =
				'https://newsapi.org/v2/everything?' +
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
				});

			this.searchQ = '';
			this.sortCriteria = '';
		},
		sortBy: function(arr, sortCrit) {
			return arr.sort(function(a, b) {
				if (a[sortCrit] > b[sortCrit]) return 1;
				if (a[sortCrit] < b[sortCrit]) return -1;
				return 0;
			});
		},
	},
	computed: {
		sortedArticles: function() {
			if (this.sortCriteria) {
				return this.sortBy(this.articles, this.sortCriteria);
			}
			return this.articles;
		},
	},
	components: {
		'app-article': Article,
		'app-search': Search,
	},
	mounted: function() {
		this.getNews(this.searchQ);
	},
};
</script>

<style lang="scss" scoped>
#app {
	font-family: 'Avenir', Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: center;
	color: #2c3e50;
	margin-top: 60px;

	h1 {
		font-size: 4rem;
	}
}</style
>>
