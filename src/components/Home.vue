<template>
    <div class="container">
        <SourceSelection @sourceChanged="sourceChanged"></SourceSelection>
        <NewsList :source="source"></NewsList>
    </div>
</template>

<script>
    import SourceSelection from './SourceSelection.vue'
    import NewsList from './NewsList.vue'

    export default {
        components: {
            SourceSelection,
            NewsList
        },
        data() {
            return {
                source: ""
            }
        },
        methods: {
            sourceChanged(source) {
                this.source = source
            }
        }
    }
</script>

<style>

</style>