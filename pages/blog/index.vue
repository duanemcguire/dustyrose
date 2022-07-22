<template>
<div>
  <div class="container d-md-flex align-items-stretch mt-3">
  <div>
    <div class="">
      <h1 style="font-size: 1.9em">Blog</h1>
      <blog-cards :blogs="blogs" :allIDs="allIDs"/>

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
    params,
    route


  }) {
    var blogs = await $content('blog', {
        text: true
      })
      .limit(20)
      .sortBy('date', 'desc')
      .fetch()
    var allIDs = []
    blogs.forEach(function(item){
      allIDs.push(item.id)
    })
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
      allYears,
      allIDs
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
          content: 'Collection of blog posts about piano work'
        },


      ]
    }
  },
}
</script>
