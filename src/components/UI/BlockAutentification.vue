<template>
    <div>
        <my-button @click="$emit('update:showReg', true)" class="aut">Регистрация</my-button>
        <my-button @click="$emit('update:showAut', true)" class="aut">Авторизация</my-button>
    </div>
</template>

<script>
import MyButton from "@/components/UI/MyButton.vue";

export default {
    components: {MyButton},
    props:{
        showReg:{type:Boolean, default:false},
        showAut:{type:Boolean, default:false},
    }
}
</script>

<style scoped>

</style>