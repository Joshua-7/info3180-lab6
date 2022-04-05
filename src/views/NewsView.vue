<template>
 <div class="news container">
 <h2>News</h2>
 </div>
 <NewsList />
 </template>

<script>
import NewsList from '@/components/NewsList.vue'
export default {
 data() {
 return {};
 },
 components: { NewsList }
};
</script>
<style>
    .news.container {
        padding-left: 600px; 
        padding-bottom: 10px;
    }
</style>