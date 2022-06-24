<template>
  <div class="container d-md-flex align-items-stretch ">
    <div class="pt-2" style="background-color: ">

        <h1 >About Me</h1>
        <p style="">

      My name is JD Kohler—I am a Piano Technician with a love for pianos.
      <BR/><BR/>
      I’m located in Clinton, Utah and strongly welcome the adventures of traveling throughout Northern Utah to tune pianos for others.
<BR/><BR/>
      As an avid piano player, I began playing at the age of 11 and understand the importance and benefits of a well-tuned piano.
<BR/><BR/>
      Having lived a military life and raised a family, I have taught piano to all ages for over 25 years, from the USA to Okinawa, Japan.
<BR/><BR/>
      Now retired as a piano teacher, I pursued my love for pianos even further and studied to become a piano technician; I am passionate about giving the best service to all pianos.
<BR/><BR/>
      Contact me today to discover how I can help you!
    </p>
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
