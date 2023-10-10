<template>
<h2>{{text}}</h2>
</template>
<script>
export default {
   name: 'AtomHeader',
  props: {
    text: {
      type: String,
      default: ''
    },
  },

}
</script>
<style>
  
</style>