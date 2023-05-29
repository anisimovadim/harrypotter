<template>
  <option value=" " disabled>{{text}}</option>
  <option v-for="option in sortOptions" :value="option.value" :key="option.value">{{option.name}}</option>
</template>

<script>
export default {
  props:{
    option:{
      type:Object
    },
      text:{
        type: String
      },

    sortOptions:{
      type:Array,
      default: ()=>[]
    }
  }
}
</script>

<style scoped>

</style>