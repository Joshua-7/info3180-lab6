<template>
<form @submit.prevent="searchNews" class="d-flex flex-column justify-content-center">
 <div class="input-group mx-sm-3 mb-2">
 <label class="visually-hidden" for="search">Search</label>
 <input type="search" name="search" v-model="searchTerm"
id="search" class="form-control mb-2 mr-sm-2" placeholder="Enter
search term here" />
 <button class="btn btn-primary mb-2">Search</button>
 </div>
 <p class="search-results">You are searching for {{ searchTerm }}</p>
 </form>
<div class="block">
    <ul class="news__list">
    <li  class="news__item" v-for="article in articles">
        <div class="card" style="width: 35rem;">
            <img class="card-img-top" :src = "article.urlToImage" alt="News image">
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
 return {articles: [],searchTerm: ''};
 },
created() {
    let self = this;
    fetch('https://newsapi.org/v2/top-headlines?country=us',
    {
        headers: {
            'Authorization': `Bearer ${import.meta.env.VITE_NEWSAPI_TOKEN}`,
    }
    })
    .then(function(response) {
        return response.json();
    })
    .then(function(data) {
        console.log(data);
        self.articles = data.articles;
    });
    },
methods: {
    searchNews() {
        let self = this;
        fetch('https://newsapi.org/v2/everything?q='+
            self.searchTerm + '&language=en', {
            headers: {
            'Authorization': `Bearer ${import.meta.env.VITE_NEWSAPI_TOKEN}`,
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
 }

};
</script>

<style>
#app {
    padding: 30px;
}
.search-results {
    text-align: center;
}

.news__list {
 display: grid; 
    grid-template-columns: repeat(3,1fr);
    grid-auto-rows: auto;
    grid-gap: 1rem;
    padding: 30px;
    list-style-type: none;
}
</style>
