<template>
  <div>
    <div v-for="post in posts" :key="post.id">
      <strong>{{ post.title }}</strong>
      <p>{{ post.body }}</p>
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
        body: "Some awesome body...",
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