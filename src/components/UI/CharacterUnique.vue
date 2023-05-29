<template>
    <div class="item">
        <div class="main-img"><img src="" alt=""></div>
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
            <ul>
                <li>Дерево: {{character.wand.wood}}</li>
                <li>Ядро: {{character.wand.core}}</li>
                <li>Длина: {{character.wand.length}} дьюм</li>
            </ul>
        </div>
        <strong>Актер: {{character.actor}}</strong>
    </div>
</template>

<script>
export default {
    props:{
        character:{
            type: Object
        },
    },

}
</script>

<style scoped>
.item{

}
</style>