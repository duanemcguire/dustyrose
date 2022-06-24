<template>
<div >
  <div class="container d-md-flex align-items-stretch mt-3">
    <div>
        <div >
          <h1 style="font-size: 1.9em">Year: {{ year }}</h1>
          <blog-cards :blogs="blogs" />
        </div>
        <div style="float: left">
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
    var blogs = await $content('blog')
    .sortBy('date', 'desc')
    .fetch()
    blogs = blogs
      .filter(blog => blog.hasOwnProperty('date'))
      .filter(blog => blog.date.split('-')[0] == params.slug)

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



    const year = params.slug
    return {
      year,
      blogs,
      allYears,
    }
  },
  head() {
    return {
       title: 'Year ' + this.year,
       meta: [
         // hid is used as unique identifier. Do not use `vmid` for it as it will not work
         {
           hid: 'year-collection',
           name: 'description',
           content: 'Collection of blog posts from ' + this.year
         }
       ]
     }
   },
}
</script>
