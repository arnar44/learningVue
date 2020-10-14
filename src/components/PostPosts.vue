<template>
  <div class="postPosts">
    <div class="postCard">
        <h3>Post Maker</h3>
        <div class="postForm">
            <input v-model="userTitle" placeholder="Title" />
            <input v-model="userBody" placeholder="Text" />
            <button @click="postToApi()" class="buttonPost">Post</button>
            <p v-if="isPosting">Posting your post...</p>
            <p v-else-if="postingError">Something went wrong posting :(</p>
            <p v-else-if="postSuccess">Post Successful!</p>
        </div>
    </div>
  </div>
</template>

<script>
import Axios from 'axios'

export default {
    name: 'PostPosts',
    data() {
        return {
            userTitle: null,
            userBody: null,
            isPosting: false,
            postingError: false,
            postSuccess: false,
        }
    },
    methods: {
        postToApi() {
            this.setState(true, false, false);

            let userPost = {
                userId: 1,
                title: this.userTitle,
                body: this.userBody
            };
                        
            Axios.post('https://jsonplaceholder.typicode.com/posts', userPost)
                .then(res => {

                    if (!res.data || !res.data.id) {
                        throw 'Unanticipated response from API';
                    }

                    userPost.id = res.data.id;
                    this.$emit('click', userPost);
                    this.setState(false, false, true);
                })
                .catch(() => {
                    this.setState(false, true, false);
                });
                
        },
        setState(working, err, succ) {
            this.isPosting = working;
            this.postingError = err;
            this.postSuccess = succ;
        }
    }
}
</script>

<style>
    .postPosts {
        height: 100%;
        width: 50%;

        padding-left: 15px;
    }

    .postCard {
        padding: 0 15px 0 15px;
    }

    .postForm {
        display: flex;
        flex-direction: column;
    }

    input {
        padding: 5px;
        margin-bottom: 15px;
    }
</style>