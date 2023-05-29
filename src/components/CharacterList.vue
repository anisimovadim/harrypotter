<template>
    <div class="wrapper">
        <ul class="carousel">
            <character-item :character="character"
                            :key="character.id"
                            :show1="show"
                            v-for="(character) in characters"
                            @give="this.$emit('give', character)"
                            @send="this.$emit('send', show, character)"
            ></character-item>
        </ul>
    </div>
</template>

<script>
import CharacterItem from "@/components/CharacterItem.vue";
export default {
    components: {CharacterItem},
    props:{
        characters:{
            type:Array,
            required:true
        },
        show:{
            type:Boolean,
            default:false
        },
      indexCharacter:{
          type: Number
      },
    },
}
</script>

<style scoped>
.wrapper{
    display: flex;
    align-items: center;
    justify-content: center;
    max-width: 1000px;
    width: 100%;
    margin: auto;
    margin-top: 50px;
}
.carousel{
    display: grid;
    grid-auto-flow: column;
    align-items: center;
    gap: 16px;
    overflow-x: scroll;
    scroll-behavior: smooth;
    scroll-snap-align: center;
}
@media screen and (max-width: 770px){
    .carousel{
        grid-auto-columns: calc((100% / 2) - 7px);
    }
}
@media screen and (max-width: 500px){
    .carousel{
        grid-auto-columns: 100%;
        gap: 5px;
    }
}
</style>