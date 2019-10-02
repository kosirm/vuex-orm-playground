<template>
  <div>
    <div v-for="post in posts" :key="post.id">
      <p class="msg-title"><strong>{{ post.title }}</strong></p>
      <p class="msg-body">{{ post.body }}</p>
      <em>By: {{ post.author.name }}</em>
    </div>
  </div>
</template>

<script>
import Post from "@/models/Post";

export default {
  name: "Posts",
  props: {
    msg: String
  },
  computed: {
    posts() {
      return Post.query().with("author").get();
    }
  },
  created() {
    // Assuming this data structure is the response from the API backend.
    const posts = [
      {
        id: 1,
        title: "Hello, world!",
        body: "I just want to let you know...",
        author: {
          id: 1,
          name: "John Doe",
          email: "john@example.com"
        }
      },
      {
        id: 2,
        title: "Hello, vuex-orm!",
        body: "That vuex-orm is...",
        author: {
          id: 1,
          name: "John Doe",
          email: "john@example.com"
        }
      },
      {
        id: 3,
        title: "Hello, world!",
        body: "AWESOME!",
        author: {
          id: 1,
          name: "John Doe",
          email: "john@example.com"
        }
      }
    ];
    Post.insert({ data: posts });
  }
};
</script>
<style>
.msg-body {color:red; font-size:200%;}
.msg-title{
  padding-top:20px; color: green;
}
</style>