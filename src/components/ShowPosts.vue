<template>
    <div class="showPosts">
        <div class="controls">
            <h3>Post Viewer</h3>
            <div class="buttonDiv">
                <button @click="getPosts()" class="buttonPost">Get Posts</button>
                <button @click="clearPosts()" class="buttonClear">Clear Posts</button>
            </div>
        </div>
        <div class="posts">
            <p v-if="isError">Sorry, error getting posts :(</p>
            <p v-else-if="isLoading">Loading posts...</p>
            <div v-else-if="posts.length !== 0" class="postsList">
                <div v-for="post in posts" :key="post.id">
                    <h5 v-text="post.title" class="postTitle" />
                    <p v-text="post.body" class="postBody" />
                </div>
            </div>
            <p v-else>No Posts to show yet!</p>
        </div>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    name: 'ShowPosts',
    props: {
        posted: Object
    },
    data() {
        return {
            isLoading: false,
            isError: false,
            posts: []
        }
    },
    methods: {
        getPosts() {
            this.isError = false;
            this.isLoading = true;
            axios.get('https://jsonplaceholder.typicode.com/posts')
                .then( res => {
                    this.isLoading = false;
                    if(!res.data) {
                        throw 'No data key fetched data';
                    }
                    this.posts = res.data
                })
                .catch( () => {
                    this.isLoading = false;
                    this.isError = true;
                });
        },
        clearPosts() {
            this.posts = [];
        }
    },
    watch: {
        // Arrow functions cannot be used for watchers!
        posted: function(newVal) {
            // API is not really posting, need to adjust IDs if user posts more than one post
            if(this.posts.length !== 0) {
                let newId = 1 + this.posts[this.posts.length - 1].id;
                newVal.id = newId;
            }
            this.posts.push(newVal);
        }
    }

}
</script>

<style>
    .showPosts {
        height: 100%;
        width: 50%;

        display: flex;
        flex-direction: column;
    }

    .controls {
        padding-bottom: 30px;
    }

    .posts {
        overflow: auto;
    }

    .posts::-webkit-scrollbar {
        height: 10px;
        width: 10px;
    }

    /* Track */
    .posts::-webkit-scrollbar-track {
        background: #f1f1f1;
    }

    /* Handle */
    .posts::-webkit-scrollbar-thumb {
        background: #888;
    }

    /* Handle on hover */
    .posts::-webkit-scrollbar-thumb:hover {
        background: #555;
    }

    .buttonDiv {
        display: flex;
        justify-content: space-evenly;
    }

    .buttonPost {
        border-radius: 5px;
        font-weight: 700;
        font-size: 1em;
        padding: 5px;
        background-color: #62C370;
        color: #fff;
        cursor: pointer;
    }

    .buttonClear {
        border-radius: 5px;
        font-weight: 700;
        font-size: 1em;
        padding: 5px;
        background-color: #D33F49;
        color: #fff;
        cursor: pointer;
    }

    .postTitle, .postBody {
        text-align: start;
    }

</style>