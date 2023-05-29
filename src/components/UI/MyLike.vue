<template>
  <div class="like">
      <input type="checkbox"
             :id="inputId" class="custom-checkbox"
             :value="characterValue"
             @change="giveCharacter"
      >
      <label :for="inputId"></label>
  </div>
</template>

<script>
export default {
props:{
  characterValue:{
    type:String,
    default: ''
  },
  inputId:{
    type: String,
    default:''
  },
    characterObject:{
      type:Object
    }
},
    methods:{
      giveCharacter(){
          this.$emit('give', this.characterObject)
      }
    }
}
</script>
<style scoped>
.custom-checkbox {
    position: absolute;
    z-index: -1;
    opacity: 0;
    width: 30px;
    height: 30px;
}
.custom-checkbox+label {
    display: inline-flex;
    align-items: center;
    user-select: none;
}
.custom-checkbox+label::before {
    content: '';
    display: inline-block;
    width: 30px;
    height: 30px;
    flex-shrink: 0;
    flex-grow: 0;
    margin-right: 0.5em;
    background-image: url("/src/assets/img/heart-regularWhite.svg");
    background-repeat: no-repeat;
    background-position: center center;
    background-size: contain;
}
.custom-checkbox:checked+label::before {
    background-image: url("/src/assets/img/heart-solidWhite.svg");
    background-position: center center;
    background-size: contain;
}
</style>