<template>
<div>
  <div class="container d-md-flex align-items-stretch mt-3">
    <div class="">
      <h1>Year</h1>
      <div v-for="year in allYears">
        <a v-bind:href = "'/year/' + year">{{year}}</a>
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
    var blogs = await $content('blog')
      .only(['date'])
      .fetch()
    blogs = blogs
      .filter(blog => blog.hasOwnProperty('date'))

    var allYears = []
    var thisYear = ''

    blogs.forEach(function(item){
      thisYear = item.date.split('-')[0]
      if (!allYears.includes(thisYear)){
        allYears.push(thisYear)
      }
    })
    allYears.sort((a,b) => (a < b) ? 1 : -1)

    return {
      allYears
    }
  },
  head() {
    return {
      title: 'Blog - McGuire Piano',
      meta: [
        // hid is used as unique identifier. Do not use `vmid` for it as it will not work
        {
          hid: 'blog-index',
          name: 'description',
          content: 'Collection of blog posts about piano rebuilding and restoration'
        }
      ]
    }
  },
}
</script>
