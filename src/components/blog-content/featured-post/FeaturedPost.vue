<template lang="">
<div class="p-4 p-md-5 mb-4 text-white rounded bg-image" id="featured">
    <div class="col-md-6 px-0">
      <template v-if="loading">
      <div class="spinner-border text-light" role="status">
        <span class="visually-hidden">Loading...</span>
      </div>
      </template>
      <template v-else-if="error">
        <h2>Unable to load featured post data, try refresh the page and load later ...</h2>
      </template>
      <template v-else>
        <h1 class="display-4 fst-italic blog-title">{{ title }}</h1>
        <p class="lead my-3 blog-body">{{ body }}</p>
        <p class="lead mb-0"><a href="#" class="text-white fw-bold">Continue reading...</a></p>
      </template>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  data() {
    return {
      id: "",
      title: "",
      body: "",
      loading: false,
      error: false,
    }
  },
  mounted() {
    this.loading = true
    this.error = false
    axios
      .get("https://jsonplaceholder.typicode.com/posts/81")
      .then(response => {
        this.loading = false
        if (response.status === 200) {
          return response.data
        } else {
          throw Error()
        }
      }, error => {
        this.loading = false
        this.error = true
        console.error("Unable to fetch featured post", error)
        throw error
      })
      .then(({ id, title, body }) => {
        this.id = id
        this.title = title
        this.body = body
      })
  }
}
</script>

<style lang="css" scoped>
#featured {
  display: flex;
  align-items: center;
  min-height: 400px;
  background-image: url("@/assets/images/components/blog-content/featured-post/background-image.webp");
}

.blog-title:first-letter,
.blog-body:first-letter {
  text-transform: capitalize;
}
</style>