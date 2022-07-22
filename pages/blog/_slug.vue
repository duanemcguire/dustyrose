<template>
<div>
  <div class="container d-md-flex align-items-stretch mt-3">
    <div id="article-content">
      <h1 style="font-size: 1.9em"> {{ blog.title }}</h1>
      <ClientOnly><prevnext :blog="blog" :dir="'blog'" /></ClientOnly>
      <BR />
      <div><time class="pubdate" :datetime="blog.date">{{blog.displayDate}}</time></div>
      <BR/>
      <nuxt-content :document="blog" />
      <photo-divs :photoset="photoset" />
      <div v-show="'tags' in blog">
        Related posts tagged as:
        <p class="tcloud" v-for="tag in blog.tags">
          <a :href="'/tag/' + tag">{{tag}}</a>
        </p>
      </div>
      <div>
        Blog posts by year:<BR/>
        <span  v-for="year in allYears">
          <a :href="'/year/' + year">{{year}}</a>&#32;
        </span>

      </div>
    </div>
    <!--<sidebar />-->
  </div>
</div>
</template>

<script>
export default {
  async asyncData({
    $content,
    params
  }) {
    const blog = await $content('blog', params.slug).fetch()
    console.log(blog.body)
    const blogs = await $content('blog')
      .only(['date'])
      .fetch()

    // build excerpt
    var str = ""
    if (typeof(blog.excerpt) == 'undefined') {
      str = blog.body.children[0].children[0].value
    } else {
      str = blog.excerpt
    }
    var maxChar = 150
    if (str) {
      str = str.trim()
      if (str.length > maxChar) {
        str = str.substr(0, maxChar - 1)
        str = str.split("").reverse().join("")
        str = str.substring(str.indexOf(" "), str.length)
        str = str.split("").reverse().join("")
      }
    }
    blog.excerpt = str
    var months = ['January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December']
    var d = new Date(blog.date + " 12:00:00")
    blog.displayDate = months[d.getMonth()] + ' ' + d.getDate().toString() + ', ' + d.getFullYear().toString()


    // establish previous and next
    const [prev, next] = await $content('blog')
      .only(['title', 'slug'])
      .sortBy('date', 'desc')
      .surround(params.slug)
      .fetch()

    const allYears = []
    var thisYear = ''
    blogs.forEach(function(item){
      thisYear = item.date.split('-')[0]
      if (!allYears.includes(thisYear)){
        allYears.push(thisYear)
      }
    })
    allYears.sort((a,b) => (a < b) ? 1 : -1)
    var photoset = []
    if (blog.hasOwnProperty('photoset')) {
      blog.photoset.forEach(function(p){
        photoset.push(p)
      })


    }





    return {
      blog,
      prev,
      next,
      allYears,
      photoset
    }
  },
  head() {
    return {
      title: this.blog.title,
      meta: [
        // hid is used as unique identifier. Do not use `vmid` for it as it will not work
        {
          hid: 'description',
          name: 'description',
          content: this.blog.excerpt
        },
        {
          hid: 'main-image',
          name: 'og:image',
          content: this.blog.img
        }
      ],
      link: [{
        rel: 'canonical',
        href: this.blog.canonical
      }, ]
    }
  },
}
</script>
<style scoped>
.comma-list {
  display: inline;
  list-style: none;
  padding: 0px;
}

.comma-list li {
  display: inline;
}

.comma-list li::after {
  content: ", ";
}

.comma-list li:last-child::after {
  content: "";
}


.tcloud a {
  line-height: 0.8;
  font-size: 0.7em;
  padding: 10px 20px;
  text-transform: uppercase;
  color: #595959;
  border: 1px solid rgba(0, 0, 0, 0.1);
  display: inline-block;
  margin: 5px;
}

.tcloud p {
  display: inline-block;
  margin-bottom: 0px;
}

figure {
  max-width: 600px;
}

.nuxt-content h2 {
  font-weight: bold;
  font-size: 28px;
}

.nuxt-content h3 {
  font-weight: bold;
  font-size: 22px;
}

.nuxt-content p {
  margin-bottom: 20px;
}

img {
  max-width: 600px;
  margin: 0 auto;

}

@media screen and (max-width: 800px) {
  img {
    max-width: 320px;
  }

  div {
    max-width: 324px;
  }

}
</style>
