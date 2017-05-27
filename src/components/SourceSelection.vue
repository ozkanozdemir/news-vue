<template>
    <div>
        <div class="jumbotron">
            <h4><i class="fa fa-list"></i> Select News Source</h4>
            <select class="form-control" @change="sourceChanged">
                <option :value="source.id" v-for="source in sources">{{ source.name }}</option>
            </select>

            <div style="margin-top:10px;" v-if="source">
                <h6>{{ source.description }}</h6>
                <a :href="source.url" target="_blank" class="btn btn-primary">
                    Go To {{ source.name }} Website
                </a>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'sourceSelection',
        data() {
            return {
                sources: [],
                source: ""
            }
        },
        created() {
            this.$http.get('https://newsapi.org/v1/sources?language=en')
                .then(res => {
                    this.sources = res.data.sources
                })
        },
        methods: {
            sourceChanged(e) {
                for (var i=0; i < this.sources.length; i++ ) {
                    if (this.sources[i].id == e.target.value) {
                        this.source = this.sources[i]
                    }
                }
                this.$emit('sourceChanged', e.target.value)
            }
        }
    }
</script>

<style>

</style>