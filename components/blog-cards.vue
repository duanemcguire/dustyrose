<template>
<div>
  <div  id="article-content" v-for="blog of blogs" :key="blog.slug" style="display: inline-block">
    <blog-card :blog="blog" />
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
    allIDs: {
      type: Array,
      required: false
    }
  },
  mounted(){
    const allIDs_string = this.$refs.allIDs.value
    this.$nuxtCookies.set('allIDs', allIDs_string, {
      path: '/',
      maxAge: 60 * 60 * 24 * 7
    })

  },
}
</script>
