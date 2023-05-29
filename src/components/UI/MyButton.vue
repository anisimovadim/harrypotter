<template>
    <button class="btn">
        <slot></slot>
    </button>
</template>

<script>
export default {

}
</script>

<style scoped>
.btn{
    width: 100%;
    height: 40px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-family: 'Inter';
    font-style: normal;
    font-weight: 400;
    font-size: 15px;
    line-height: 18px;
    letter-spacing: 0.025em;
    color: #FFFFFF;
    background: #514A92;
    border-radius: 3.65799px;
    outline: none;
    border: none;
    transition: background-color .5s;
}
.btn:hover{
    background: #423c79;
    transition: background-color .5s;
}
.btn:active{
    background: #2c275d;
    transition: background-color 0s;
}
</style>