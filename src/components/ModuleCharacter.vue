<template>
    <div class="window-character" v-if="showu" @click="this.$emit('update:showu', false)">
    <character-unique :character="character" @click.stop/>
    </div>
</template>

<script>
import CharacterUnique from "@/components/UI/CharacterUnique.vue";

export default {
    components: {CharacterUnique},
    props:{
        showu:{
            type:Boolean,
            default:false
        },
        character:{
            type: Object
        }
    }

}
</script>

<style scoped>
.window-character{
    width: 100%;
    height: 100vh;
    position: fixed;
    background-color: rgba(0, 0, 0, 0.36);
    top: 0;
    left: 0;
    z-index: 9999;
}
</style>