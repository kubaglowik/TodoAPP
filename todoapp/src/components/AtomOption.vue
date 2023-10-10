<template>
<option :value="modelValue">{{text}}</option>
</template>
<script>
export default {
      modelValue: {
      type: String,
      default: ''
}
}
</script>
<style>
  
</style>