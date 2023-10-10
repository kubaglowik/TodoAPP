<template>
<select :name="modelName" :id="modelValue">
  <slot></slot>
</select>
</template>
<script>
export default {
      modelName: {
      type: String,
      default: ''
    },
      modelId:{
        type: String,
        default: ''
      }
}
</script>
<style>
  
</style>
