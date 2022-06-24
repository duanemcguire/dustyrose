<template>
  <div class="container d-md-flex align-items-stretch ">
    <div style="width: 100%" class="pt-2" >
      <h1>Schedule Piano Tuning</h1>
      <iframe style="width: 600px; max-width: 100%; height: 600px; max-height: 95%" src="/sched-for-iframe.html"></iframe>
    </div>
    <sidebar />
  </div>

</template>
<style>
.topnav a.schedule{
  color: #eee8dc;
  text-decoration: underline;

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
