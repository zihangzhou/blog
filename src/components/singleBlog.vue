<template>
  <div id="post">
    <div id="singleBlog">
      <h1>{{ blog.title }}</h1>
      <article>{{ blog.body }}</article>
    </div>
    <div>
      <button type="button" v-on:click="returnBlogs()">
        Return
      </button>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      id: this.$route.params.id,
      blog: [],
    };
  },
  methods: {
    returnBlogs() {
      this.$router.go(-1);
    },
  },
  created() {
    axios
      .get("https://jsonplaceholder.typicode.com/posts/" + this.id)
      .then((response) => {
        this.blog = response.data;
      })
      .catch((e) => {
        console.log(e);
      });
  },
};
</script>

<style scoped>
#post {
  max-width: 800px;
  margin: 0 auto;
}

#singleBlog {
  padding: 20px;
  margin: 10px 0;
  box-sizing: border-box;
  background: rgb(212, 212, 212);
}

button {
  width: 10%;
  height: 30px;
  font-size: 20px;
  border-radius: 8px;
  margin: 10px 0 20px;
}
</style>
