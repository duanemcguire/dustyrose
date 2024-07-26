<template>
  <div class="container d-md-flex align-items-stretch ">
    <div class="pt-2" style="background-color: ">

      <h1>{{content.title}}</h1>
      <div>
      <nuxt-content :document="content" />
      </div>

      <div style="text-align: center; ">
        <img id="dusty-rose-piano" style="max-width: 60%; " :src=content.image />
      </div>
    </div>
    <sidebar />
  </div>

</template>
<style>
  .topnav a.home{
    color: #eee8dc;
    text-decoration: underline;
  }
  @media screen and (max-width: 800px) {
  #dusty-rose-piano {
    display: none;
  }

}

</style>
<script>
export default {
  async asyncData({
    $content,
    params
  }) 
  {const content= await $content('misc', 'home').fetch()
   
    return {
      content
    }
  },

  head() {
    return {
      title: 'Dusty Rose Piano',
      meta: [
        // hid is used as unique identifier. Do not use `vmid` for it as it will not work
        {
          hid: 'top',
          name: 'description',
          content: 'Dusty Rose Piano - Piano Tuning Service in Northern Utah'
        }
      ]
    }
  },
}
</script>
