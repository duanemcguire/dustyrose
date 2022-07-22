<template>
<div>
  <div class="container d-md-flex align-items-stretch mt-3">
    <div>
      <h1 style="font-size: 1.9em">{{ category.name }}</h1>
      <div id="morecategories">
        <b>All Categories:</b>&nbsp;&nbsp;
        <category-cloud :categories="categories" />
      </div>
      <blog-cards :blogs="blogs" :allIDs="allIDs" />
    </div>
  </div>
</div>
</template>

<script>
export default {

  async asyncData({
    $content,
    params
  }) {
    const category = await $content('categories', params.slug)
      .fetch()
    const categories = await $content('categories')
      .sortBy('name', 'asc')
      .fetch()
    var blogs = await $content('blog')
      .sortBy('date', 'desc')
      .fetch()
    blogs = blogs
      .filter(blog => blog.hasOwnProperty('category'))
      .filter(blog => blog.category.includes(params.slug))
    var allIDs = []
    blogs.forEach(function(item){
      allIDs.push(item.id)
    })

    return {
      category,
      categories,
      blogs,
      allIDs
    }
  },
  head() {
    return {
      title: 'Blog Category: ' + this.category.name,
      meta: [
        // hid is used as unique identifier. Do not use `vmid` for it as it will not work
        {
          hid: 'category-collection',
          name: 'description',
          content: 'Collection of piano blog posts categorized as ' + this.category.name
        },
        {
          hid: 'main-image',
          name: 'og:image',
          content: this.category.img
        }
      ],
      link: [{
        rel: 'canonical',
        href: 'https://blog.duanemcguire.com/category/' + this.category.slug
      }, ]
    }
  },
}
</script>
