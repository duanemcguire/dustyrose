<template>
<div>
{{blogs[2]}}
  <div v-for="(blog,index) of blogs" :key="blog.title">
    <a :href="'/blog-id/' + blog.id" > {{blog.title}} </a>
  </div>
</div>
</template>

<script>
export default {
  async asyncData({
    $content,
    params
  }) {
    const blogs = await $content('blog')
    .only(['id','title'])
    .fetch()
    return {
      blogs
    }
  }
}
</script>
