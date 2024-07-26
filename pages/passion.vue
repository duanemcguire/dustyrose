<template>
  <div class="container d-md-flex align-items-stretch ">
    <div class="pt-2" style="background-color: ">

      <h1>{{content1.title}}</h1>
      <Div >
      <nuxt-content :document="content1" />
      
<div style="float: left; margin-right: 10px; margin-bottom: 10px;" ><img src="/images/david-holifield-NmyoGwkl-Tg-unsplash.jpg" style="max-width: 90vw;" /></div>
      <nuxt-content :document="content2" />

</div>
    </div>
    <sidebar />
  </div>

</template>
<style>
.topnav a.passion{
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
  {const content1= await $content('misc', 'passion1').fetch()
   const content2= await $content('misc', 'passion2').fetch()
    return {
      content1,
      content2
    }
  },
  head() {
    return {
      title: 'Passion for the Piano',
      meta: [
        // hid is used as unique identifier. Do not use `vmid` for it as it will not work
        {
          hid: 'top',
          name: 'description',
          content: 'JD Kohler\'s passion for pianos'
        }
      ]
    }
  },
}
</script>
