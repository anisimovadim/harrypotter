<template>
    <div class="item">
        <span></span>
        <div class="main-img"><img src="" alt=""></div>
        <character-item :character="character"/>
        <div class="block-text">
            <ul>
                <li>Факультет: {{character.house}}</li>
                <li>Волшебник: {{character.wizard}}</li>
                <li>Дата рождения: {{character.dateOfBirth}}</li>
                <li>Родословная: {{character.ancestry}}</li>
                <li>Патронус: {{character.patronus}}</li>
                <li>Студент хогвартса: {{character.hogwartsStudent}}</li>
            </ul>
            <div class="line"></div>
            <strong>Информация о палочке</strong>
            <ul class="wand">
                <li>Дерево: {{character.wand.wood}}</li>
                <li>Ядро: {{character.wand.core}}</li>
                <li>Длина: {{character.wand.length}} дьюм</li>
            </ul>
        </div>
        <strong class="actor">Актер: {{character.actor}}</strong>
    </div>
</template>

<script>
import CharacterItem from "@/components/CharacterItem.vue";

export default {
    components: {CharacterItem},
    props:{
        character:{
            type: Object
        },
    },

}
</script>

<style scoped>
.item{
    background-color: #242633;
    width: max-content;
    padding: 30px;
    margin: auto;
    margin-top: 10%;
    font-size: 24px;
    display: flex;
    align-items: flex-start;
    gap: 30px;
    position: relative;
    padding-bottom: 95px;
}
span{
    width: 105%;
    height: 106%;
    border: white 1px solid;
    position: absolute;
    top: -2.7%;
    left: -2.5%;
}
.wand{
    margin-top: 20px;
}
.line{
    width: 100%;
    height: 1px;
    background-color: #ffffff;
    margin: 20px 0;
}
ul{
    list-style: none;
    display: flex;
    flex-direction: column;
    gap: 10px;
}

.actor{
    position: absolute;
    bottom: 20px;
    text-align: center;
    left: 30%;
}
</style>