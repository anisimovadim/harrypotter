<template>
  <div class="likes-box">
    <strong>Избранное:</strong>
      <div class="flex-box">
        <span >Волшебники: {{countWizard}}</span>
        <span>Маглы: {{countNoWizard}}</span>
      </div>
  </div>
</template>

<script>
export default {
  props:{
    countWizard: {
      type:Number,
      default: 0
    },
    countNoWizard:{
      type:Number,
      default: 0
    }
  }
}
</script>

<style scoped>
strong{
  font-family: 'JejuMyeongjo';
  font-size: 25px;
}
.flex-box{
  font-family: 'Inter';
  display: flex;
  gap: 20px;
  align-items: center;
}
</style>