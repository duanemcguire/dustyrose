<template>
<div>
  <div class="container d-md-flex align-items-stretch mt-3">
    <div>
      <h1 style="font-size: 1.9em">Categories</h1>
      <div>
        <ul>
          <li v-for="cat of category" :key="category.slug">
            <NuxtLink :to="'/category/' + cat.slug">
              {{ cat.name }}
            </NuxtLink>
          </li>
        </ul>
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
    const category = await $content('categories', params.slug)
      .fetch()
    return {
      category
    }
  },
  head() {
    return {
      title: 'Blog Category: ' + this.category.name,
      meta: [
        // hid is used as unique identifier. Do not use `vmid` for it as it will not work
        {
          hid: 'description',
          name: 'description',
          content: 'Categories of this blog'
        }
      ],
      link: [{
        rel: 'canonical',
        href: 'https://blog.duanemcguire.com/category/'
      }, ]
    }
  }
}
</script>
