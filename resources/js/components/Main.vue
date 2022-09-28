<template>
  <main>
    <div class="container">
      <div class="row mt-5">
        <div class="col mt-5">
            <h1>Recent posts:</h1>
            <div class="posts">
                <div class="row">
                    <PostCard v-for="post in posts" :key="post.id" :post="post" />
                </div>
            </div>
        </div>
      </div>
    </div>
  </main>
</template>

<script>
import PostCard from './PostCard.vue';
import axios from 'axios';

export default {

    components: {
        PostCard,
    },

    data: function(){
        return{
            posts: [],
            currentPage: 1,
            lastPage: null,
            loading: false,
        }
    },

    methods: {

        getPosts(postsPage = 1){
            axios.get('/api/posts' , {
                page: postsPage
            }).then((response) => {
                console.log(response.data.results);
                this.posts = response.data.results.data;
                this.currentPage = response.data.results.current_page;
                this.lastPage = response.data.results.last_page;
                this.loading = false;
            }).catch((error) => {
                console.error(error);
            })
        }
    },

    created(){
        this.getPosts();
    }
};
</script>

<style>
</style>