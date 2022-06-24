<template>
  <div class="container d-md-flex align-items-stretch ">
    <div style="width: 100%" class="pt-2" >
      <h1 style="font-size: 1.5em; margin-top: 7px;">Schedule Piano Tuning</h1>
      <iframe style="width: 600px; max-width: 100%; height: 600px; max-height: 95%" src="/sched-for-iframe.html"></iframe>
    </div>
    <sidebar />
  </div>

</template>
<style>
  .topnav a.schedule{
    border-bottom: 1px solid white;
    padding-bottom: 2px;
  }
</style>
<script>
export default {
  head() {
    return {
      title: 'Schedule tuning with Dusty Rose Piano',
      meta: [
        // hid is used as unique identifier. Do not use `vmid` for it as it will not work
        {
          hid: 'top',
          name: 'description',
          content: 'Schedule Piano Tuning'
        }
      ]
    }
  },
}
</script>
