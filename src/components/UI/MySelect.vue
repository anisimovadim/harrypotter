<template>
    <select class="custom-select" :value="myalue">
        <slot></slot>
    </select>
</template>

<script>
export default {
    props:{
        titleForSelect:{
            type:String
        },
        myalue:{
            type:String,
        }
    },
}
</script>

<style scoped>
.custom-select{
    width: 130px;
    height: 40px;
    background: #414359;
    border-radius: 3px;
    font-family: 'Inter';
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
}
</style>