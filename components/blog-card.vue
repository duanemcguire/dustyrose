<template>
<div class="blog-card card" @click="goItem">
  <a :href="'/blog/' + blog.slug">
    <img class="card-img-top img-fluid" :src="thumbnail" :alt="blog.caption">
  </a>
  <div class="card-body" @click="goItem">
    <a :href="'/blog/' + blog.slug">
      <div class="card-title">{{blog.title}}</div>
    </a>
    <div class="blog-card-excerpt">{{postExcerpt}}</div>


  </div>

</div>
</template>

<script>
export default {
  props: {
    blog: {
      type: Object,
      required: true
    }
  },
  data() {
    function reverseString(str) {
      return str.split("").reverse().join("");
    }

    function excerptBuild(obj, n) {
      var str = ""
      if (typeof(obj.excrpt) == 'undefined') {
        str = obj.body.children[0].children[0].value
      } else {
        str = obj.excrpt
      }

      if (str) {
        str = str.trim()
        if (str.length > n) {
          str = str.substr(0, n - 1)
          str = reverseString(str)
          str = str.substring(str.indexOf(" "), str.length)
          str = reverseString(str) + '...'
        }
      }
      return str
    }
    var months = ['January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December']
    var d = new Date(this.blog.date + " 12:00:00")
    const displayDate = months[d.getMonth()] + ' ' + d.getDate().toString() + ', ' + d.getFullYear().toString()

    const description = excerptBuild(this.blog, 100)
    var thumbnail = ''
    if (this.blog.hasOwnProperty('img') && this.blog.img > "") {
      thumbnail = this.blog.img
    }else{
      if (this.blog.hasOwnProperty('photoset') ) {
        this.blog.photoset.forEach(function(item){
          if('thumbnail' in item){
            thumbnail = item.path
            var tArr = thumbnail.split('/')
            var fn = tArr[tArr.length-1]
            thumbnail = '/images/thumb/' + fn
          }
        })

      }
    }



    return {
      postExcerpt: description,
      displayDate: displayDate,
      thumbnail: thumbnail


    }
  },
  methods: {
    goItem() {
      location.href = "/blog/" + this.blog.slug
    }
  }
}
</script>
<style>
.blog-card {
  margin-right: 10px;
  margin-bottom: 10px;
  float: left;
  height: 25rem;
  width: 20rem;
  overflow: hidden;
  background-color: #eeeeee;
  border: 2px solid black;
}

.blog-card a {
  text-decoration: none;
  color: black
}

.blog-card:hover {
  width: 21rem;
}

.blog-card a:hover {
  color: blue;
}

.blog-card-excerpt {
  width: 18rem;
  height: 5rem;
  overflow: hidden;
  text-overflow: ellipsis;
  margin: 0;
}

.blog-card img {
  height: 240px;
  width: auto;
  overflow: hidden;
}

.card-title {
  font-size: 1.1rem;
  font-weight: bold;
  height: 1.5rem;
  overflow: hidden;
}
</style>
