<template>
<button @input="$emit('@click')">{{text}}</button>
</template>
<script>
export default {
   name: 'AtomButton',
   text:{
    type:String,
    default: " "
   }

}
</script>
<style>
  
</style>