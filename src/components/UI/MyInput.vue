<template>
    <input type="text" class="custom-input"
           :placeholder="myplaceholder"
           :value="myvalue"
    />
</template>

<script>
export default {
props:{
  myplaceholder:{
    type:String
  },
  myvalue:{
      type:String,
  }
}
}
</script>

<style scoped>
.custom-input{
    width: 300px;
    height: 40px;
    background: #414359;
    border: none;
    outline: none;
    border-radius: 3px;
    font-style: normal;
    font-weight: 400;
    font-size: 17.2542px;
    line-height: 21px;
    letter-spacing: -0.065em;
    color: rgba(255, 255, 255, 0.4);
    padding: 10px;
    background-image: url("/src/assets/img/searchLogo.svg");
    background-repeat: no-repeat;
    background-position-y: center;
    background-position-x: 99%;
}
</style>