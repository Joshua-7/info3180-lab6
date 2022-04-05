<template>
<div class="block">
    <ul class="news__list">
        <li  class="news__item" v-for="article in articles">
        <div class="card" style="width: 18rem;">
            <img class="card-img-top" :src = "article.urlToImage" alt="Card image cap">
            <div class="card-body">
                <h3 class="card-text">{{ article.title }}</h3>
                <p class="card-text">{{ article.description }}</p>
            </div>
        </div>
        </li>
    </ul>
</div>
</template>
<script>
export default {
 data() {
 return {articles: []};
 },
 created() {
    let self = this;
    fetch('https://newsapi.org/v2/top-headlines?country=us',
    {
        headers: {
            'Authorization': `Bearer f41afdd44447452db1214769de5b70bd`,
    }
    })
    .then(function(response) {
        return response.json();
    })
    .then(function(data) {
        console.log(data);
        self.articles = data.articles;
    });
    }
};
</script>
