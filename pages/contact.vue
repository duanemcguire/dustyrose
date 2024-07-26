<template>
<div >
  <div class="container d-md-flex align-items-stretch ">
    <div style="width: 100%">

    <h1 >{{content.title}}</h1>

      <nuxt-content :document="content" />


    </div>
  </div>
</div>
</template>
<style>
.topnav a.contact{
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
  {const content= await $content('misc', 'contact').fetch()
   
    return {
      content
    }
  },


  head() {
    return {
       title: 'Dusty Rose Piano Contact Information',
       meta: [
         // hid is used as unique identifier. Do not use `vmid` for it as it will not work
         {
           hid: 'contact-page',
           name: 'description',
           content: 'Contact information for Dusty Rose Piano and JD Kohler'
         }
       ]
     }
   }
}
</script>
