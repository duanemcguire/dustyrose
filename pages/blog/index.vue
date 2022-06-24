<template>
<div>
  <div class="container d-md-flex align-items-stretch mt-3">
  <div>
    <div class="">
      <h1 style="font-size: 1.9em">Blog</h1>
      <time class="pubdate" datetime="2008-09-01" style="display: none;">September 1, 2008</time>
      <div id="morecategories">
        <b>Categories&nbsp;&nbsp;</b>
        <category-cloud :categories="categories" />
      </div>
      <blog-cards :blogs="blogs" />

    </div>
    <div style="clear: both; float:left">
      Blog posts by year:<BR/>
      <span  v-for="year in allYears">
        <a :href="'/year/' + year">{{year}}</a>&#32;
      </span>
    </div>
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
    var blogs = await $content('blog', {
        text: true
      })
      .only(['title', 'description', 'img', 'slug', 'excerpt', 'body'])
      .limit(20)
      .sortBy('date', 'desc')
      .fetch()


    const categories = await $content('categories')
      .sortBy('name', 'asc')
      .fetch()

      var blogYears = await $content('blog')
          .only('date')
          .fetch()
      blogYears = blogYears
          .filter(blog => blog.hasOwnProperty('date'))
      var allYears = []
      var thisYear = ''

      blogYears.forEach(function(item){
        thisYear = item.date.split('-')[0]
        if (!allYears.includes(thisYear)){
          allYears.push(thisYear)
        }
      })
      allYears.sort((a,b) => (a < b) ? 1 : -1)


    return {
      blogs,
      categories,
      allYears
    }
  },
  head() {
    return {
      title: 'Blog - Dusty Rose Piano',
      meta: [
        // hid is used as unique identifier. Do not use `vmid` for it as it will not work
        {
          hid: 'blog-index',
          name: 'description',
          content: 'Collection of blog posts about piano technology'
        },

      ]
    }
  },
}
</script>
