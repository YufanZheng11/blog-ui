<template>
  <BlogHeader />
  <BlogContent />
</template>

<script>
import BlogHeader from './components/blog-header/BlogHeader.vue'
import BlogContent from './components/blog-content/BlogContent.vue'

export default {
  name: 'App',
  components: {
    BlogHeader,
    BlogContent
  }
}
</script>

<style>
</style>
