<template>
<div>
<client-only>
<script> {{cmd}} </script>
</client-only>
</div>
</template>

<script>
export default {
  async asyncData({
    $content,
    params
  }) {
    const blogs = await $content('blog')
    .fetch()
    var blog = Object
    var tag = ''
    var loc = ''
    var cmd = ''
    blogs.forEach(function(item){
      if(item.id == params.id){
        blog = item
        loc = "/blog/" + item.slug
        cmd = "window.location.href = '" + loc + "'"
      }
    })
    return {
      loc, cmd
    }
  }
}
</script>
