<template>
<button @button="$emit('@click')">{{text}}</button>
</template>
<script>
export default {
   name: 'AtomButton',
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