<template>
    <div class="col-4">
        <b-card
            v-bind:img-src="data.urlToImage"
            v-bind:img-alt="data.title"
            img-top
            tag="article"
            style="max-width: 20rem;"
            class="mb-2"
        >
            <b-card-title>{{ limitChar(data.title) }}</b-card-title>
            <b-card-sub-title>{{ data.author }} | {{ data.source.name }}</b-card-sub-title>
            <b-card-text>
            {{ limitChar(data.description) }}
            </b-card-text>

            <b-button v-bind:href="data.url" variant="primary">View Article</b-button>
        </b-card>
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