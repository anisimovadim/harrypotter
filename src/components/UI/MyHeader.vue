<template>
  <header>
    <div class="main">
      <div class="sorts-block">
<!--sort-->
        <my-select :myalue="valueOption1" @change="changeValue1">
          <select-sort :sort-options="sortOptions1" :text="text1"/>
        </my-select>
<!--filters-->

<!--bigLittle-->
        <my-select :myalue="valueOption2" @change="changeValue2">
          <select-sort :sort-options="sortOptions2"/>
        </my-select>
      </div>


      <div class="logo">
        <img src="../../assets/img/logo.svg" alt="LOGO">
      </div>

      <my-input :class="'search'" :myplaceholder="'Search'" :myvalue="valueSearch" @input="setValue" class="input"/>

        <div class="grids">
            <my-select :myalue="valueOption3" @change="changeValue3">
                <select-sort :sort-options="sortOptions3" :text="text3"/>
            </my-select>

            <my-select :myalue="valueOption4" @change="changeValue4">
                <select-sort :sort-options="sortOptions4" :text="text4"/>
            </my-select>

            <my-select :myalue="valueOption5" @change="changeValue5">
                <select-sort :sort-options="sortOptions5" :text="text5"/>
            </my-select>
        </div>
    </div>
  </header>
</template>

<script>
import MySelect from "@/components/UI/MySelect.vue";
import MyInput from "@/components/UI/MyInput.vue";
import SelectSort from "@/components/SelectSort.vue";
export default {
components:{MySelect, MyInput, SelectSort},
  props:{
      text1:{
          type:String
      },
      text2:{
          type:String
      },
      text3:{
          type:String
      },
      text4:{
          type:String
      },
      text5:{
          type:String
      },
      sortOptions1:{
        type:Array,
        default: ()=>[]
      },
      valueOption1:{
          type: String,
      },
      sortOptions2:{
          type:Array,
        default: ()=>[]
      },
      valueOption2:{
          type: String,
      },
      sortOptions3:{
          type:Array,
          default: ()=>[]
      },
      valueOption3:{
          type: String,
      },
      sortOptions4:{
          type:Array,
          default: ()=>[]
      },
      valueOption4:{
          type: String,
      },
      sortOptions5:{
          type:Array,
          default: ()=>[]
      },
      valueOption5:{
          type: String,
      },
      valueSearch:{
        type:String,
      }
  },
  methods:{
      changeValue1(e){
        console.log(this.valueOption1)
        this.$emit('update:valueOption1', e.target.value)
      },
      changeValue2(e){

        this.$emit('update:valueOption2', e.target.value)
      },
      changeValue3(e){

          this.$emit('update:valueOption3', e.target.value)
      },
      changeValue4(e){

          this.$emit('update:valueOption4', e.target.value)
      },
      changeValue5(e){

          this.$emit('update:valueOption5', e.target.value)
      },
      setValue(e){

        this.$emit('update:valueSearch', e.target.value)
      }
  }
}
</script>

<style scoped>
header{
  width: 100%;
  padding: 25px 112px;
  background: #242633;
}
.header .main{
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 20px;
}
.logo{
  width: 150px;
  height: auto;
}
.logo img{
  width: 150px;
  height: auto;
}
.input{
    width: 200px;
}
.grids{
    display: grid;
    grid-template-rows: 1fr 1fr 1fr;
    gap: 20px;
}
.sorts-block{
    display: flex;
    align-items: center;
    gap: 20px;
}
.search{
    background-image: url("/src/assets/img/searchLogo.svg");
    background-repeat: no-repeat;
    background-position-y: center;
    background-position-x: 99%;
}
</style>