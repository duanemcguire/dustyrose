<template>
  <div class="caption">
    <img :src="photoinstance.path" />
      {{photoinstance.caption}}
  </div>
</template>

<script>
export default {
  props: {
    photoinstance: {
      type: Object,
      required: true
    }
  }
}
</script>
<style>

</style>
