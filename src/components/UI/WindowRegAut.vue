<template>
    <div class="module" v-if="show" @click="$emit('update:show', false)">
      <slot></slot>
    </div>
</template>

<script>
export default {
    props:{
       show:{type:Boolean, default:false},
        user:{
           type:Object
        }
    }
}
</script>

<style scoped>
.module{
    width: 100%;
    position: fixed;
    top: 0;
    bottom: 0;
    left: 0;
    background-color: rgba(0, 0, 0, 0.36);
    z-index: 9999;
}
</style>