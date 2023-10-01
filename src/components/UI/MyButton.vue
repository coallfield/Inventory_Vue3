<template>
    <button 
         @mouseover="colorButton = true" 
         @mouseleave="colorButton = false" 
         :class="colorButton ? 'over-btns' : 'btns'"
         > <slot></slot>  
    </button>

</template>

<script>
export default {
    name: 'MyButton',
    data() {
        return {
            colorButton: false
        }
    }
}
</script>

<style scoped lang="scss">
    .btns {
        color: white;
        margin: 10px;
        background: none;
        border: 2px solid white;
        outline: none;
        border-radius: 5px;
        width: 10%;
        height: 5vh;   
    }
    .over-btns {
        color: black;
        margin: 10px;
        background: white;
        border: 2px solid white;
        outline: none;
        border-radius: 5px;
        width: 10%;
        height: 5vh;
    }
</style>