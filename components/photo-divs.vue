<template>
  <div>
  <div  v-for="photoinstance of photoset" >
    <photo-div :photoinstance="photoinstance" />
  </div>
</div>
</template>

<script>
export default {
  props: {
    photoset: {
      type: Array,
      required: true
    }
  },
}
</script>
