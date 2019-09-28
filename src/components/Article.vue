<template>
    <div class="col-4">
        <img 
        class="img-fluid"
        v-bind:src="data.urlToImage" 
        v-bind:alt="data.title">
        <h4 >{{ limitChar(data.title) }}</h4>
        <h6>{{ data.author }} | {{ data.source.name }}</h6>
        <p>{{ limitChar(data.description) }}</p>
    </div>
</template>

<script>
    export default {
        props: ['data'],
        methods: {
            limitChar: function(string) {
                let body = this.stripTags(string);
                return body.length > 100 ? body.substring(0, 100) + '...' : body;
            },
            stripTags: function(text) {
                return text.replace(/(<([^>]+)>)/ig, '');
            }
        }
    }
</script>

<style>

</style>