<template>
<div >
  <div class="container d-md-flex align-items-stretch ">
    <div style="width: 100%">
        <h1>Contact</h1>
        <BR/><BR/>
        <div>
          <p><strong>JD Kohler, Piano Tuner-Technician<br>
            Dusty Rose Piano<br>Clinton, UT 84015<br></strong><BR/>
            <span class="hover">dustyrosepiano@outlook.com</span><BR/>
            <span class="hover">(360) 632-4380</span> text + call<BR/>
            <BR/>
            Serving All of Northern Utah
          </p>
        </div>
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
