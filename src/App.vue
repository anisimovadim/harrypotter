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
        <block-autentification v-if="!identification" v-model:show-reg="showsReg" v-model:show-aut="showsAut"/>
        <user-log v-if="identification" v-model:data="dataUser"/>
        <likes-component v-if="identification" :count-wizard="this.characters.filter(i=>i.check===true && i.wizard===true).length"
                       :count-no-wizard="this.characters.filter(i=>i.check===true && i.wizard!==true).length"
                       class="likes-box"
                         />
        <character-list v-model:idenf1="identification" @give="checks" @send="send" :characters="searchingCharacter"/>
        <module-character v-model:showu="shows" v-model:character="characterForModule"/>
        <window-reg-aut v-model:show="showsReg">
            <module-registration
                    @createuser="registr"
                    v-model:email1="email"
                    v-model:gender1="gender"
                    v-model:last-name1="lastName"
                    v-model:last-name21="lastName2"
                    v-model:name1="name"
                    v-model:number-phone1="numberPhone"
                    v-model:year1="year"
                    v-model:login1="login"
                    v-model:password1="password"
                    v-model:error1="er1"
                    v-model:error2="er2"
                    v-model:error3="er3"
                    v-model:error4="er4"
                    v-model:error5="er4"
                    v-model:error6="er6"
                    v-model:error7="er7"
                    v-model:error8="er8"
                    v-model:error9="er9"
                    :genderOption="sortOptions3"
                    v-model:value-gender="valueGender"
                    v-model:close-show="showsReg"
                   />
        </window-reg-aut>
        <window-reg-aut v-model:show="showsAut">
            <module-autorization v-model:value1="valueLogin" v-model:value2="valuePsw" @senduser="autorization"/>
        </window-reg-aut>
    </div>
  </div>
</template>

<script>
import CharacterList from "@/components/CharacterList.vue";
import MyHeader from "@/components/UI/MyHeader.vue";
import LikesComponent from "@/components/LikesComponent.vue";
import ModuleCharacter from "@/components/ModuleCharacter.vue";
import WindowRegAut from "@/components/UI/WindowRegAut.vue";
import ModuleRegistration from "@/components/ModuleRegistration.vue";
import BlockAutentification from "@/components/UI/BlockAutentification.vue";
import ModuleAutorization from "@/components/ModuleAutorization.vue";
import UserLog from "@/components/UserLog.vue";
export default {
    components: {
        UserLog,
        ModuleAutorization,
        BlockAutentification,
        ModuleRegistration, WindowRegAut, ModuleCharacter, CharacterList, MyHeader, LikesComponent},
    data(){
        return{
            characters:[],
            characterChecks: '',
            characterForModule:{},
            shows:false,
            showsReg:false,
            showsAut:false,
            valueGender: ' ',
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
                {value: 'male', name: 'мужской'},
                {value: 'female', name: 'женский'},
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
            pt:[],
            identification: false,
            dataUser:[],
            name:'',
            lastName: '',
            lastName2: '',
            email: '',
            numberPhone: '',
            gender: '',
            year: '',
            login:'',
            password:'',
            valueLogin:'',
            valuePsw:'',
            er1:false,
            er2:false,
            er3:false,
            er4:false,
            er5:false,
            er6:false,
            er7:false,
            er8:false,
            er9:false,
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
        },
        registr(user, show){

            let regexp4 = /^8\([0-9]{3}\)[0-9]{3}-[0-9]{2}-[0-9]{2}$/g;
            let regexp5 = /^[a-z]{4,}@[a-z]{3,}.(ru|com|inbox)$/g;
            this.er1=!/^[А-Я]{1}[а-я]{1,}$/g.test(user.name);
            this.er2=!/^[А-Я]{1}[а-я]{1,}$/g.test(user.lastName);
            this.er3=!/^[А-Я]{1}[а-я]{1,}$/g.test(user.lastName2);
            this.er4=!regexp5.test(user.email);
            this.er5=!regexp4.test(user.numberPhone);
            this.er6 =  !Boolean(this.valueGender !== ' ');
            this.er7 = !Boolean((+this.year)>=10);
            this.er8=!Boolean(user.login.length>5);
            this.er9=!Boolean(user.password.length>8);
            console.log(this.er7)
            let c = 0
            if (!this.er1 && !this.er2 && !this.er3 && !this.er4 && !this.er5 && !this.er7 && !this.er6) {
                for (let i =0; i<localStorage.length;i++){
                    const key = localStorage.key(i);
                    const user1 = JSON.parse(localStorage[key]);
                    if (user.email===user1.email || user.numberPhone===user1.numberPhone || user.password===user1.password || user.login===user1.login){
                        alert('Пользователь уже существует');
                        c=1
                        break
                    }
                }
                if (c!==1){
                    localStorage.setItem(user.id, JSON.stringify(user));
                    show=false
                    this.showsReg=show
                }
            }

            this.name='';
            this.lastName= '';
            this.lastName2= '';
            this.email= '';
            this.numberPhone= '';
            this.gender= '';
            this.year= '';
            this.valueGender=' ';
            this.password='';
            this.login='';

        },
        autorization(login, password){
            console.log(login)
            for (let i = 0; i<localStorage.length;i++){
                const key = localStorage.key(i);
                const user = JSON.parse(localStorage[key]);
                if (user.login===login && user.password===password){
                    this.identification=true;
                    this.dataUser.push(user.lastName);
                    this.dataUser.push(user.name);
                    this.showsAut=false
                    break
                }
            }
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