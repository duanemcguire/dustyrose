<template>
<div>
  <div id="article-content" v-for="blog of blogs" :key="blog.slug" style="display: inline-block">
    <blog-card :blog="blog" :dir="dir"/>
  </div>
</div>
</template>

<script>
export default {
  props: {
    blogs: {
      type: Array,
      required: true
    },
    dir: {
      type: String
    }
  }
}
</script>
