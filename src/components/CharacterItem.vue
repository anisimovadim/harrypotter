<template>
    <li @click="sendCharacter">
      <div class="block-img">
        <span class="borderLine" v-if="character.image"></span>
        <div class="img"><img :src="character.image" alt="img" v-if="character.image"></div>
        <div class="img blackBg" v-if="!character.image">
            <span></span>
            <img src="../assets/img/placeholder.png">
        </div>


        <my-like v-if="idenf" @click.stop :input-id="character.name.replace(' ','-')" class="likes"
                 :class="character.name.replace(' ','-')"
                 :character-value="JSON.stringify(character)"
                 @give="this.$emit('give', character)"
        />

        <span class="linear" v-if="character.image"></span>
      </div>
        <strong>{{character.name}}</strong>
    </li>
</template>

<script>
import MyLike from "@/components/UI/MyLike.vue";
export default {
  components: {MyLike},
  props:{
    character:{
      type: Object,
      required:true
    },
      show1:{
        type: Boolean,
          default:false
      },
      idenf:{
        type:Boolean,
          default: false
      }
  },
    methods:{
      sendCharacter(){
          this.$emit('send', this.show1, this.character);
      }
    }
}
</script>

<style scoped>
li{
    position: relative;
    list-style: none;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
  padding-bottom: 60px;
    cursor: pointer;
}
li .img img{
    width: 250px;
    height: 350px;
    object-fit: cover;
    object-position: top;
}
.block-img{
  position: relative;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  margin: auto;

}
.borderLine{
  position: absolute;
  width: 89%;
  height: 90%;
  border: white 1px solid;
  top: 4%;
  left: 5%;
  z-index: 2;
}
.linear{
  position: absolute;
  width: 100%;
  height: 30%;
  bottom: 0;
  background: linear-gradient(180deg, #10141B 20.83%, rgba(16, 20, 27, 0) 100%);
  transform: matrix(1, 0, 0, -1, 0, 0);
}
strong{
  position: absolute;
  font-family: 'JejuMyeongjo';
  font-style: normal;
  font-weight: 400;
  font-size: 22px;
  line-height: 32px;
  bottom: 10px;
}
.likes{
  position: absolute;
  right: 15px;
  bottom: 25px;
  z-index: 99;
}
.blackBg span{
    background-color: rgba(44, 39, 93, 0.53);
    width: 250px;
    height: 350px;
    position: absolute;
    top: 0;
    left: 0;
    bottom: 0;
}
</style>