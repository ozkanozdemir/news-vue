<template>
    <div>
        <ul class="media-list">
            <li class="media" v-for="article in articles">
                <div class="media-left">
                    <a :href="article.url" target="_blank">
                        <img :src="article.urlToImage" class="media-object rounded">
                    </a>
                </div>
                <div class="media-body">
                    <h4 class="media-heading">
                        <a :href="article.url" target="_blank">{{ article.title }}</a>
                    </h4>
                    <h5><i>by {{ article.author }}</i></h5>
                    <p>{{ article.description }}</p>
                </div>
            </li>
        </ul>
    </div>
</template>

<script>
    export default {
        name: 'newsList',
        props: ['source'],
        data() {
            return {
                articles: []
            }
        },
        methods: {
            updateSource(source) {
              this.$http.get('https://newsapi.org/v1/articles?source=' + source+ '&apiKey=9df7106e801c404e9b6c71e83a047322')
                  .then(res => {
                      this.articles = res.data.articles
                  })
          }
        },
        watch: {
            source(val) {
                this.updateSource(val)
            }
        }
    }
</script>

<style scoped>
    .media-left img {
        width: 128px;
        margin-right: 10px;
    }
    .media {
        border-top: 1px solid lightgrey;
        padding-top: 20px;
    }
</style>