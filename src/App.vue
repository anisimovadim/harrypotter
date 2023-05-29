<template>
  <div class="container">
    <div class="content">
        <my-header class="header"
                 :sort-options1="sortOptions1"
                 v-model:value-option1="valueOption1"
                 :sort-options2="sortOptions2"
                 v-model:value-option2="valueOption2"
                 :sort-options3="sortOptions3"
                 v-model:value-option3="valueOption3"
                 v-model:value-search="mainValueSearch"
                 :sort-options4="sortOptions4"
                 v-model:value-option4="valueOption4"
                 :sort-options5="sortOptions5"
                 v-model:value-option5="valueOption5"
                 :text1="'Выберите сортировку'"
                 :text3="'Фильтр по гендеру'"
                 :text4="'Фильтр по факультету'"
                 :text5="'Фильтр по патронусу'"
        ></my-header>
        <likes-component :count-wizard="this.characters.filter(i=>i.check===true && i.wizard===true).length"
                       :count-no-wizard="this.characters.filter(i=>i.check===true && i.wizard!==true).length"
                       class="likes-box"
                         />
        <character-list @give="checks" @send="send" :characters="searchingCharacter"/>
        <module-character v-model:showu="shows" v-model:character="characterForModule"/>
    </div>
  </div>
</template>

<script>
import CharacterList from "@/components/CharacterList.vue";
import MyHeader from "@/components/UI/MyHeader.vue";
import LikesComponent from "@/components/LikesComponent.vue";
import ModuleCharacter from "@/components/ModuleCharacter.vue";
export default {
    components: {ModuleCharacter, CharacterList, MyHeader, LikesComponent},
    data(){
        return{
            characters:[],
            characterChecks: '',
            characterForModule:{},
            shows:false,
            sortOptions1:[
                {dis:false, value: 'name', name: 'По имени персонажа'},
                {dis:false, value: 'actor', name: 'По имени актера'},
                {dis:false, value: 'eyeColour', name: 'По цвету глаз'},
            ],
            sortOptions2:[
                {dis:false, value: 'little', name: 'По убыванию'},
                {dis:false, value: 'big', name: 'По возрастанию'},
            ],
            sortOptions3:[
                {pole: 'gender', value: 'male', name: 'мужской'},
                {pole: 'gender', value: 'female', name: 'женский'},
            ],
            sortOptions4:[
                {value: 'Gryffindor', name: 'Gryffindor'},
                {value: 'Slytherin', name: 'Slytherin'},
                {value: 'Hufflepuff', name: 'Hufflepuff'},
                {value: 'Ravenclaw', name: 'Ravenclaw'},
            ],
            sortOptions5:[],
            valueOption1: ' ',
            valueOption2: 'big',
            valueOption3: ' ',
            valueOption4: ' ',
            valueOption5: ' ',
            mainValueSearch: '',
            arrayLikesing: [],
            pt:[]
        }
    },
    methods:{
        async getApi(){
            const res = await fetch('https://hp-api.onrender.com/api/characters');
            this.characters=await res.json();
            this.characters.forEach(i=> {
                i.check = false;
                if (i.patronus) this.pt.push(i.patronus);
            })
            this.sortOptions5.push({value: 'all', name: 'Все'})
            this.sortOptions5.push({value: '', name: 'Без патронуса'})
            this.pt = Array.from(new Set(this.pt));
            console.log(this.pt)
            this.pt.forEach(i => this.sortOptions5.push({value: i, name: i}));

        },
        checks(character){
            character.check=!character.check
            console.log(character)
        },
        send(sh, ch){
            sh=true
            this.shows=sh
            this.characterForModule=ch
            console.log(sh)
            console.log(this.shows)
        }

    },
    mounted() {
        this.getApi()
    },
  computed:{
      sortingList(){
        if (this.valueOption2==='big') {
          return [...this.characters].sort((p, q) => p[this.valueOption1]?.localeCompare(q[this.valueOption1]));
        }
        else if(this.valueOption2==='little') {
          return [...this.characters].sort((p, q) => (p[this.valueOption1]?.localeCompare(q[this.valueOption1]) || ((+p[this.valueOption1])-(+q[this.valueOption1])))).reverse();
        }
        else {
          return [...this.characters].sort((p, q) => p[this.valueOption1]?.localeCompare(q[this.valueOption1]));
        }
      },
      filterGender(){
            if (this.valueOption3!==' ') return this.sortingList.filter(i=>i.gender.toLowerCase()===this.valueOption3)
            else return this.sortingList
      },
      filterHouse(){
          console.log(this.valueOption4)
          if (this.valueOption4!==' ') return this.filterGender.filter(i=>i.house.toLowerCase()===this.valueOption4.toLowerCase())
          else return this.filterGender
      },
      filterPt(){
          console.log(this.valueOption5)
          if (this.valueOption5===' ' || this.valueOption5==='all') return this.filterHouse
          else return this.filterHouse.filter(i=>i.patronus.toLowerCase()===this.valueOption5.toLowerCase())
      },
    searchingCharacter(){
        return this.filterPt.filter(c => (c.actor.toLowerCase().includes(this.mainValueSearch.toLowerCase())) || (c.name.toLowerCase().includes(this.mainValueSearch.toLowerCase())))
    }
  }
}
</script>

<style scoped>
@font-face {
  src: url("assets/fonts/JejuMyeongjo-Regular.ttf");
  font-family: 'JejuMyeongjo';
}
.container{
  width: 100%;
  background-image: url("/src/assets/img/bg.svg");
  background-position: center;
  background-size: contain;
}
.likes-box{
  width: 1000px;
  margin: auto;
  margin-top: 40px;
  display: flex;
  flex-direction: column;
  gap: 10px;
  font-size: larger;
}
</style>