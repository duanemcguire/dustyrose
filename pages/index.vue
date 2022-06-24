<template>
  <div class="container d-md-flex align-items-stretch ">
    <div class="pt-2" style="background-color: ">

      <h1 style="font-size: 1.5em; margin-top: 7px;">JD Kohler, Piano Tuner-Technician</h1>
      <p>Pianos are my life, and no day is complete without playing.
        I tune and maintain pianos, so that each customer may find the joy in their piano that I find in mine.
      </p>
        <p>
        How's your piano sounding?  Does it need a little help?   <a href="/schedule">Schedule your piano tuning</a> today and
        fall in love with your piano again.
        Basic tuning services start at just $100.

      </p>

      <img id="dusty-rose-piano" style="max-width: 100%; opacity: 0.5;" src="/images/dusty-rose-piano.png" />

    </div>
    <sidebar />
  </div>

</template>
<style>
  .topnav a.home{
    border-bottom: 1px solid white;
    padding-bottom: 2px;
  }
  @media screen and (max-width: 800px) {
  #dusty-rose-piano {
    display: none;
  }

}

</style>
<script>
export default {
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
