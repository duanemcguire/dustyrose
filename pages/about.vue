<template>
  <div class="container d-md-flex align-items-stretch ">
    <div class="pt-2" style="background-color: ">

    <h1 >{{content.title}}</h1>

      <nuxt-content :document="content" />

    </div>
    <sidebar />
  </div>

</template>
<style>
.topnav a.about{
  color: #eee8dc;
  text-decoration: underline;

}
</style>
<script>
export default {
  async asyncData({
    $content,
    params
  }) 
  {const content= await $content('misc', 'about').fetch()
   
    return {
      content
    }
  },

  head() {
    return {
       title: 'About Dusty Rose Piano',
       meta: [
         // hid is used as unique identifier. Do not use `vmid` for it as it will not work
         {
           hid: 'contact-page',
           name: 'description',
           content: 'About Dusty Rose Piano and JD Kohler'
         }
       ]
     }
   }
}
</script>
