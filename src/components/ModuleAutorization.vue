<template>
    <div>
        <form @click.stop>
        <h2>Регистрация</h2>
        <div class="data-input">
            <my-input :myplaceholder="'Логин'" :myvalue="value1" @input="(e)=>$emit('update:value1', e.target.value)"/>
            <my-input :myplaceholder="'Пароль'" :myvalue="value2" @input="(e)=>$emit('update:value2', e.target.value)"/>
        </div>
        <my-button @click.prevent="$emit('senduser', value1, value2)">Войти</my-button>
        </form>
    </div>
</template>

<script>
import MyInput from "@/components/UI/MyInput.vue";
import MyButton from "@/components/UI/MyButton.vue";

export default {
    components: {MyButton, MyInput},
    props:{
        value1:{type:String, default:''},
        value2:{type:String, default:''},
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
    margin-top: 10%;
}
.data-input{
    display: flex;
    flex-direction: column;
    gap: 20px;
}
.data-input input{
    width: 100%;
}
</style>