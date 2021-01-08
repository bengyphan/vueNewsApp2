<template>
	<div class="d-flex">
		<input
			type="text"
			class="p-2 w-50"
			placeholder="SEARCH"
			v-model.lazy="searchQ"
			@change="changeNews"
		/>
		<!-- <button v-on:click="changeNews">Submit</button> -->
	</div>
</template>
<script>
export default {
	data: function() {
		return {
			searchQ: '',
		};
	},
	methods: {
		changeNews: function() {
			this.$emit('newsChanged', this.searchQ);
			this.searchQ = '';
		},
	},
};
</script>
