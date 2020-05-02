<template>
  <div id="showBlogs">
    <h1>All Blog Articles</h1>
    <input type="text" v-model="search" placeholder="Search blogs" />
    <div
      v-for="(blog, index) in displayedBlogs"
      v-bind:key="index"
      class="singleBlog"
    >
      <router-link v-bind:to="'/blog/' + blog.id"
        ><h2>{{ blog.title }}</h2>
      </router-link>
      <article>{{ blog.body | snippet }}</article>
    </div>
    <nav aria-label="Page navigation bar">
      <ul class="pagination">
        <li class="page-item">
          <button
            type="button"
            class="page-link"
            v-if="page != 1"
            v-on:click="page--"
          >
            Previous
          </button>
        </li>
        <li class="page-item">
          <button
            type="button"
            class="page-link"
            v-for="(pageNumber, index) in pages.slice(page - 1, page + 5)"
            v-bind:key="index"
            v-on:click="page = pageNumber"
          >
            {{ pageNumber }}
          </button>
        </li>
        <li class="page-item">
          <button
            type="button"
            class="page-link"
            v-if="page < pages.length"
            v-on:click="page++"
          >
            Next
          </button>
        </li>
      </ul>
    </nav>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      blogs: [],
      filtered: [],
      page: 1,
      perPage: 9,
      pages: [],
      search: "",
    };
  },
  methods: {
    setPages(blogs) {
      let numberOfPages = Math.ceil(blogs.length / this.perPage);
      this.pages = [];
      for (let index = 1; index <= numberOfPages; index++) {
        this.pages.push(index);
      }
    },
    paginate(blogs) {
      let page = this.page;
      let perPage = this.perPage;
      let from = page * perPage - perPage;
      let to = page * perPage;
      return blogs.slice(from, to);
    },
  },
  computed: {
    displayedBlogs() {
      if (!this.search) {
        return this.paginate(this.filtered);
      } else {
        return this.paginate(this.filteredBlogs);
      }
    },
    filteredBlogs() {
      return this.blogs.filter((blog) => {
        return blog.title.match(this.search) || blog.body.match(this.search);
      });
    },
  },
  watch: {
    filtered() {
      this.setPages(this.filtered);
    },
  },
  created() {
    axios
      .get("https://jsonplaceholder.typicode.com/posts")
      .then((response) => {
        this.blogs = response.data;
        this.filtered = this.blogs;
      })
      .catch((e) => {
        console.log(e);
      });
  },
  beforeUpdate() {
    this.filtered = this.filteredBlogs;
  },
  filters: {
    snippet: function(value) {
      if (value.length < 100) {
        return value;
      } else {
        return value.slice(0, 100) + "...";
      }
    },
  },
};
</script>

<style scoped>
#showBlogs {
  max-width: 800px !important;
  margin: 0 auto;
}

.singleBlog {
  padding: 20px;
  margin: 20px 0;
  box-sizing: border-box;
  background: rgb(212, 212, 212);
}

input {
  width: 100%;
  height: 50px;
  font-size: 30px;
}

li {
  display: inline-block;
}

button.page-link {
  font-size: 20px;
  color: #29b3ed;
  font-weight: 500;
}
</style>
