<template>
    <div>
        <input type="text" placeholder="SEARCH"
        v-model="searchQ"
        @change.lazy="changeNews">
        <!-- <button v-on:click="changeNews">Submit</button> -->
    </div>
</template>
<script>
export default {
    data: function() {
        return {
            searchQ: ''
        }
    },
    methods: {
        changeNews: function() {
            this.$emit("newsChanged", this.searchQ);
            this.searchQ = '';
        }
    }
}
</script>
<style>

</style>