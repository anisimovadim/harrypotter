<template>
    <div>
        <ul>
            <li>{{data[0]}}</li>
            <li>{{data[1]}}</li>
        </ul>
    </div>
</template>

<script>
export default {
    props:{
        data:{
            type:Array,
            default:()=>[]
        }
    }
}
</script>

<style scoped>
div{
    width: 1000px;
    margin: auto;
    margin-top: 20px;
    display: flex;
    justify-content: flex-end;
}
ul{
    list-style: none;
    display: flex;
    align-items: center;
    gap: 10px;
}
</style>