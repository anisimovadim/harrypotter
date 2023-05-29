<template>
    <form @click.stop>
        <h2>Регистрация</h2>
        <div class="data-input">
            <my-input :class="{error:error1}" type="text" placeholder="Имя" :myvalue="name1" @input="setinput1"/>
            <my-input :class="{error:error2}" type="text" placeholder="Фамилия" :myvalue="lastName1" @input="(e)=>$emit('update:lastName1', e.target.value)"/>
            <my-input :class="{error:error3}" type="text" placeholder="Отчество" :myvalue="lastName21" @input="(e)=>$emit('update:lastName21', e.target.value)"/>
            <my-input :class="{error:error4}" type="text" placeholder="Email" :myvalue="email1" @input="(e)=>$emit('update:email1', e.target.value)"/>
            <my-input :class="{error:error5}" type="text" placeholder="Номер телефона" :myvalue="numberPhone1" @input="(e)=>$emit('update:numberPhone1', e.target.value)"/>
            <my-input :class="{error:error8}" type="text" placeholder="Логин" :myvalue="login1" @input="(e)=>$emit('update:login1', e.target.value)"/>
            <my-input :class="{error:error9}" type="text" placeholder="Пароль" :myvalue="password1" @input="(e)=>$emit('update:password1', e.target.value)"/>
        </div>
        <div class="data-else">
            <my-select :class="{error:error6}" :myalue="valueGender" @change="(e)=>$emit('update:valueGender', e.target.value)">
                <select-sort :text="'Пол'" :sort-options="genderOption"/>
            </my-select>
            <my-input :class="{error:error7}" type="text" placeholder="Возраст" class="year" :myvalue="year1" @input="(e)=>$emit('update:year1', e.target.value)"/>
        </div>
        <div class="data-house">
            <label for="Gryffindor">
                <span>Гриффендор</span>
                <input type="checkbox" name="Gryffindor" id="Gryffindor" value="Gryffindor" v-model="user.likeHouse">
            </label>
            <label for="Slytherin">
                <span>Слизерин</span>
                <input  type="checkbox" name="Slytherin" id="Slytherin" value="Slytherin" v-model="user.likeHouse">
            </label>
            <label for="Hufflepuff">
                <span>Пуффендуй</span>
                <input  type="checkbox" name="Hufflepuff" id="Hufflepuff" value="Hufflepuff" v-model="user.likeHouse">
            </label>
            <label for="Ravenclaw">
                <span>Когтевран</span>
                <input type="checkbox" name="Ravenclaw" id="Ravenclaw" value="Ravenclaw" v-model="user.likeHouse">
            </label>
        </div>
        <my-button @click.prevent="sendUser">Зарегистрироваться</my-button>
    </form>
</template>

<script>
import SelectSort from "@/components/SelectSort.vue";
import MyButton from "@/components/UI/MyButton.vue";
import MyInput from "@/components/UI/MyInput.vue";
import MySelect from "@/components/UI/MySelect.vue";


export default {
    components: {MySelect, MyButton, SelectSort, MyInput},
    props:{
        name1: {type:String},
        lastName1: {type:String},
        lastName21: {type:String},
        email1: {type:String},
        numberPhone1: {type:String},
        gender1: {type:String},
        year1: {type:String},
        login1: {type: String},
        password1: {type: String},
        error1:{type:Boolean, default:false},
        error2:{type:Boolean, default:false},
        error3:{type:Boolean, default:false},
        error4:{type:Boolean, default:false},
        error5:{type:Boolean, default:false},
        error6:{type:Boolean, default:false},
        error7:{type:Boolean, default:false},
        error8:{type:Boolean, default:false},
        error9:{type:Boolean, default:false},
        valueGender:{type:String, default:' '},
        genderOption:{type:Array},
        closeShow:{type:Boolean, default:false}
    },
    data(){
        return{
            user:{
                name: this.name1,
                lastName: this.lastName1,
                lastName2: this.lastName21,
                email: this.email1,
                numberPhone: this.numberPhone1,
                gender: this.gender1,
                year: this.year1,
                likeHouse: [],
                login: this.login1,
                password: this.password1
            },
        }
    },
    methods:{
        sendUser(){
            this.user.id = Date.now();
            this.user.name=this.name1
            this.user.lastName=this.lastName1
            this.user.lastName2=this.lastName21
            this.user.email=this.email1
            this.user.numberPhone=this.numberPhone1
            this.user.gender=this.gender1
            this.user.year=this.year1;
            this.user.gender=this.valueGender;
            this.user.login=this.login1;
            this.user.password=this.password1;
            console.log(this.user)
            this.$emit('createuser', this.user, this.closeShow);
            this.user.likeHouse=[]
        },
        setinput1(e){
            this.$emit('update:name1', e.target.value)
        }
    }

}
</script>

<style scoped>
h2{
    text-align: center;
}
form{
    display: flex;
    flex-direction: column;
    width: 500px;
    background-color: #242633;
    padding: 50px;
    gap: 30px;
    margin: auto;
    margin-top: 2%;
}
.data-input{
    display: flex;
    flex-direction: column;
    gap: 20px;
}
.data-input input{
    width: 100%;
}
.data-else{
    display: flex;
    align-items: center;
    justify-content: space-between;
}
.data-house{
    display: grid;
    grid-template-columns: 1fr 1fr;
    align-items: center;
    justify-content: center;
    width: max-content;
    margin: auto;
    column-gap: 50px;
    row-gap: 10px;
    font-size: 20px;
}
.data-house label{
    display: flex;
    align-items: center;
    width: max-content;
}
.data-house label span{
    width: 130px;
}
.year{
    width: 90px;
}
.error{
    border: 1px solid red;
}
</style>